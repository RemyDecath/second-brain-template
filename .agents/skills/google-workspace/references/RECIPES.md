# `gws` recipes — per-service reference

Load this only when `SKILL.md` doesn't already answer the question.

Every command below assumes `gws` is on `$PATH` and authenticated — check with
`scripts/gws-auth-hint.sh`. If it is not, that script prints the fix; the login
command it suggests is:

```bash
gws auth login --scopes openid,email,profile,https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/spreadsheets,https://www.googleapis.com/auth/documents,https://www.googleapis.com/auth/presentations,https://www.googleapis.com/auth/gmail.modify,https://www.googleapis.com/auth/calendar
```

Give it to the user to run — never run it yourself, it prints a consent URL
and then waits for a human to open it in a browser and approve. Keep the scope list in sync with `GWS_LOGIN_SCOPES` in
`scripts/gws-auth-hint.sh`.

## Discovering an API before calling it

Never guess parameter names — the CLI mirrors the Google Discovery documents:

```bash
gws <service> --help                    # resources + methods for a service
gws schema <service>.<resource>.<method>  # required params, types, defaults
gws schema drive.files.list --resolve-refs
```

## Global flags worth knowing

| Flag | Use |
|---|---|
| `--params '{...}'` | URL / query parameters |
| `--json '{...}'` | Request body (POST/PATCH/PUT) |
| `--format json\|table\|yaml\|csv` | `csv` and `table` are far cheaper than `json` |
| `--dry-run` | Validate locally without calling the API |
| `-o <path>` | Write binary/exported responses to a file (**must be inside the CWD**) |
| `--upload <path>` | Upload file content (multipart) |
| `--page-all` | Auto-paginate as NDJSON — expensive, use `--page-limit` |

## Drive

```bash
# Search — always cap pageSize and mask fields
gws drive files list --params '{
  "q": "name contains \"roadmap\" and trashed = false",
  "pageSize": 20,
  "fields": "files(id,name,mimeType,modifiedTime,webViewLink)"
}'

# Files in a folder
gws drive files list --params '{"q": "\"<FOLDER_ID>\" in parents and trashed = false", "pageSize": 50, "fields": "files(id,name,mimeType)"}'

# Metadata only
gws drive files get --params '{"fileId": "<ID>", "fields": "name,mimeType,owners,modifiedTime,webViewLink"}'

# Shared drives are excluded by default
gws drive files list --params '{"q": "...", "supportsAllDrives": true, "includeItemsFromAllDrives": true}'
```

Useful `q` operators: `name contains`, `fullText contains`, `mimeType =`,
`'<id>' in parents`, `modifiedTime > '2026-01-01T00:00:00'`, `trashed = false`,
`sharedWithMe`, `starred`.

## Docs

```bash
# Read → prefer scripts/gws-fetch.sh (Markdown export, ~100x cheaper)
scripts/gws-fetch.sh <url>

# Structural read (only when you need styles, headings, tabs, comments)
gws docs documents get --params '{"documentId": "<ID>", "fields": "title,body.content.paragraph.elements.textRun.content"}'

# Create
gws docs documents create --json '{"title": "Sprint 42 review"}'

# Append text (helper)
gws docs +write --document <ID> --text "## Findings"

# Structured edit
gws docs documents batchUpdate --params '{"documentId": "<ID>"}' \
  --json '{"requests": [{"insertText": {"location": {"index": 1}, "text": "Hello\n"}}]}'
```

## Sheets

```bash
# Read a range as CSV — much cheaper than the default JSON envelope
gws sheets spreadsheets values get --format csv \
  --params '{"spreadsheetId": "<ID>", "range": "Backlog!A1:H200"}'

# List the tabs before guessing a range
gws sheets spreadsheets get --params '{"spreadsheetId": "<ID>", "fields": "sheets.properties(title,gridProperties)"}'

# Append rows
gws sheets spreadsheets values append \
  --params '{"spreadsheetId": "<ID>", "range": "Backlog!A1", "valueInputOption": "USER_ENTERED"}' \
  --json '{"values": [["Story", "Status"], ["Checkout v2", "Done"]]}'

# Overwrite a range
gws sheets spreadsheets values update \
  --params '{"spreadsheetId": "<ID>", "range": "Backlog!B2", "valueInputOption": "USER_ENTERED"}' \
  --json '{"values": [["In review"]]}'
```

> **Shell gotcha:** a range like `Backlog!A1` contains `!`, which zsh expands as
> history. Inside the single-quoted JSON above it is safe; never put a bare
> `Sheet1!A1` in double quotes in an interactive zsh.

## Slides

```bash
# Whole deck as text  → scripts/gws-fetch.sh <url>          (no slide boundaries!)
# One slide's text     → scripts/gws-slide-text.sh <url> <n>
# Deck outline         → scripts/gws-slide-text.sh <url> --outline
# One slide as an image→ scripts/gws-slide-png.sh <url> <n>

# Slide inventory without the multi-MB payload
gws slides presentations get --params '{"presentationId": "<ID>", "fields": "title,slides.objectId"}'

# Text of one slide, raw (what gws-slide-text.sh wraps)
gws slides presentations pages get --params '{"presentationId": "<ID>", "pageObjectId": "<SLIDE_ID>", "fields": "pageElements(shape(text(textElements(textRun(content)))))"}'

# Speaker notes for one slide
gws slides presentations pages get --params '{"presentationId": "<ID>", "pageObjectId": "<SLIDE_ID>", "fields": "slideProperties.notesPage"}'

# Create a deck
gws slides presentations create --json '{"title": "Quarterly review"}'
```

> A full `slides presentations get` on a 47-slide deck returns **~16 MB** of
> JSON. Always use a `fields` mask, or export instead.
>
> The Drive `text/plain` export of a presentation contains **no slide
> delimiters**, so it cannot answer "what is on slide N?" — use
> `gws-slide-text.sh` for anything slide-scoped.
>
> Slides splits one paragraph into several styled `textRun`s, sometimes
> mid-word, so concatenate the runs before splitting on their newlines.
> Both bundled scripts already do this.

## Gmail

```bash
# Search (ids only) then fetch what you need
gws gmail users messages list --params '{"userId": "me", "q": "from:sre newer_than:7d", "maxResults": 10}'

# Headers + snippet — cheap triage
gws gmail users messages get --params '{"userId": "me", "id": "<MSG_ID>", "format": "metadata", "metadataHeaders": ["From","To","Subject","Date"]}'

# Full body (expensive — base64url payload parts)
gws gmail users messages get --params '{"userId": "me", "id": "<MSG_ID>", "format": "full"}'

# Threads
gws gmail users threads get --params '{"userId": "me", "id": "<THREAD_ID>", "format": "metadata"}'

# Labels
gws gmail users labels list --params '{"userId": "me"}'
gws gmail users messages modify --params '{"userId": "me", "id": "<MSG_ID>"}' \
  --json '{"addLabelIds": ["<LABEL_ID>"], "removeLabelIds": ["INBOX"]}'
```

Search operators: `from:`, `to:`, `subject:`, `has:attachment`, `newer_than:7d`,
`older_than:1m`, `is:unread`, `label:`, `in:anywhere`.

The granted scope is `gmail.modify`: read, send, label and archive — **never
permanent deletion**. A `messages delete` call will return `403`; use
`messages trash` if the user explicitly asks.

## Calendar

```bash
gws calendar +agenda                         # today, human-readable

gws calendar events list --params '{
  "calendarId": "primary",
  "timeMin": "2026-08-01T00:00:00Z",
  "timeMax": "2026-08-08T00:00:00Z",
  "singleEvents": true,
  "orderBy": "startTime",
  "maxResults": 25,
  "fields": "items(id,summary,start,end,attendees(email,responseStatus),hangoutLink)"
}'

gws calendar events insert --params '{"calendarId": "primary"}' \
  --json '{"summary": "Design review", "start": {"dateTime": "2026-08-03T10:00:00+02:00"}, "end": {"dateTime": "2026-08-03T11:00:00+02:00"}, "attendees": [{"email": "personne@example.com"}]}'

gws calendar freebusy query --json '{"timeMin": "...", "timeMax": "...", "items": [{"id": "personne@example.com"}]}'
```

`singleEvents: true` expands recurring events — without it you get the
recurrence rule instead of the occurrences.

## Cross-service helpers

```bash
gws workflow +standup-report     # today's meetings + open tasks
gws workflow +meeting-prep       # next meeting: agenda, attendees, linked docs
gws workflow +weekly-digest      # this week's meetings + unread count
gws workflow +email-to-task
gws drive +upload --file ./report.md --folder <FOLDER_ID>
```

## Non-Google files stored in Drive

Drive export only works on Google-native files. For anything else, download the
bytes first, then use a local converter:

```bash
scripts/gws-fetch.sh <file-id> -o ./doc.pdf     # binary download
pdftotext -layout ./doc.pdf -                   # PDF  → text  (poppler)
pandoc ./spec.docx -t markdown -o ./spec.md     # docx → md    (pandoc)
tesseract ./journey-map.png out && cat out.txt  # image → OCR  (tesseract)
```

If the tool is missing, say so rather than falling back to guessing — and note
that `pdftotext`/`pandoc`/`tesseract` come from `poppler`/`pandoc`/`tesseract`
on Homebrew.

## Generating the full upstream skill set

The `gws` project ships ~95 generated skills (one per service, plus personas and
recipes). To get them locally:

```bash
cd <a scratch directory> && gws generate-skills
```

This writes `./skills/gws-*/SKILL.md`. Use it as an escape hatch when you need a
method this reference doesn't cover — do **not** commit it into the repo.
Upstream source: <https://github.com/googleworkspace/cli/tree/main/skills>
