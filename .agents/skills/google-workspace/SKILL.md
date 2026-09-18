---
name: google-workspace
description: >
  Read and write Google Workspace data (Drive, Docs, Sheets, Slides, Gmail, Calendar)
  through the gws CLI. Use whenever the user mentions a Google Drive file or folder, a
  Google Doc, Google Sheet, Google Slides deck, a Gmail message or thread, or a Google
  Calendar event — including when they only paste a docs.google.com, drive.google.com
  or calendar.google.com link. Never guess the content of a Google resource and never
  ask the user to copy/paste it — fetch it with gws.
license: MIT
metadata:
  audience: all
  domain: productivity
  api: cli
  mcp_required: false
  owner: your-name-or-org
  version: "2.0.0"
  last-updated: "2026-07-30"
---

# Google Workspace (`gws`)

`gws` is the single CLI for every Google Workspace API. It is a convenient way to read or write Google Workspace data from the CLI.

**Never invent the content of a Google resource, and never ask the user to
copy/paste it: fetch it.**

## When to use this skill

As soon as a request involves any of these — including when the user only pastes a link:

| Signal | Service |
|---|---|
| Drive file/folder, `drive.google.com/…` | Drive |
| Google Doc, `docs.google.com/document/…` | Docs |
| Google Sheet, `docs.google.com/spreadsheets/…` | Sheets |
| Google Slides, `docs.google.com/presentation/…` | Slides |
| Gmail message/thread/label, "my inbox" | Gmail |
| Calendar event, availability, "my agenda" | Calendar |

## Preflight

```bash
scripts/gws-auth-hint.sh   # "gws: ready (you@example.com)", or the exact fix
```

It wraps `gws auth status` and, when something is wrong, tells you *which*
thing — missing binary, missing OAuth client, or missing login — with the
command to fix it. The other scripts call it automatically on failure, so you
usually just relay their output.

- `gws: command not found` → not installed: `npm install -g @googleworkspace/cli`,
  then sign in below.
- `token_valid` is not `true`, or a call fails with `401` / "not authenticated"
  → not signed in. Sign in below.
- A `403` on one service only → the token predates a scope. The same login
  re-consents with the full set.

**Never run `gws auth login` yourself.** It prints a consent URL and then blocks
on its localhost listener until a human approves in a browser — it would hang
your turn. Instead, give the user this command and stop:

```bash
gws auth login --scopes openid,email,profile,https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/spreadsheets,https://www.googleapis.com/auth/documents,https://www.googleapis.com/auth/presentations,https://www.googleapis.com/auth/gmail.modify,https://www.googleapis.com/auth/calendar
```

Tell them what to expect, because the CLI **does not open a browser itself**:

> It prints a `https://accounts.google.com/…` URL and waits. Open that URL in
> your browser, sign in with your Google account and approve the permissions
> — the command finishes on its own once you do.

Pass the scopes in full: a bare `gws auth login` opens an interactive scope
picker and grants a narrower set, which then fails at call time. Do **not** use
`--readonly` (breaks writes) or `--full` (asks for far more than we need).

It needs `client_secret.json` in the gws config directory (`~/.config/gws/`, or
`~/Library/Application Support/gws/` on older macOS setups). The platform
installer writes it; if it is missing, re-run the installer.

Once the user confirms they are signed in, re-run `gws auth status` and carry on.

Granted scopes: Drive, Sheets, Docs, Slides, `gmail.modify` and Calendar
(read **and** write).

---

## Read documents with the scripts, not the raw API

This is the single most important rule in this skill. The document APIs return
the full structural tree of a file — every shape, every style run, every
element ID. On a real 47-slide deck, `slides presentations get` returns
**15.8 MB of JSON (~4 million tokens)**. The same deck exported as text is
**25 KB (~4.6k tokens)** — a **625×** difference for the same information.

### `scripts/gws-fetch.sh <url-or-id>` — any file as cheap text

Resolves the URL, picks the cheapest export format for that file type, writes it
to a file, and prints **only a summary** — never the content.

```bash
scripts/gws-fetch.sh "https://docs.google.com/document/d/<ID>/edit"
```
```
title:    Q3 Product Brief
kind:     document
modified: 2026-07-29T14:05:08.401Z
exported: text/markdown
path:     /var/folders/.../gws-fetch/<ID>.md
size:     18422 bytes · 402 lines · 2810 words (~3746 tokens)
```

Then **read the file selectively** — `grep` for what you need, or view a line
range. Do not `cat` a large file into context.

| File type | Exported as | Note |
|---|---|---|
| Google Doc | `text/markdown` | Headings, lists and tables preserved |
| Google Slides | `text/plain` | Whole-deck reading only — **no slide boundaries**, see below |
| Google Sheet | `text/csv` | **First sheet only** — see below for other tabs |
| Anything else | raw bytes | Download, then convert locally |

Options: `-o <path>` to choose the destination, `--mime <mime>` to force a
format, `--print` to also echo the content (small files only).

### `scripts/gws-slide-text.sh <url-or-id> <n>` — one slide's text

**The Drive text export of a deck has no slide delimiters at all**, so it can
never answer "what is on slide 6?". Use this script for anything slide-scoped.
It fetches a single page with a text-only field mask (~4 KB) and prints ~1 KB.

```bash
scripts/gws-slide-text.sh "https://docs.google.com/presentation/d/<ID>/edit" 6
scripts/gws-slide-text.sh <ID> --outline   # every slide: number, id, first line
```
```
slide:  6 of 47 (objectId g3c895a8aafd_3_0) — Organization Chart
---
Digital Organization - Macro view
Our Digital Organization is structured into four layers: …
```

`--outline` is one API call for the whole deck (~2 KB for 47 slides) — use it to
locate the right slide before reading it.

### `scripts/gws-slide-png.sh <url-or-id> <n>` — render a slide as an image

Text extraction loses diagrams, arrows and org charts. Render the slide and look
at the image.

```bash
scripts/gws-slide-png.sh "https://docs.google.com/presentation/d/<ID>/edit" 6
scripts/gws-slide-png.sh <ID> --list      # slide number → objectId
```
```
slide:    6 of 47 (objectId g3c895a8aafd_3_0)
path:     /var/folders/.../gws-fetch/<ID>-slide-06.png
size:     1600x900 px · 257980 bytes
```

Use `--size SMALL|MEDIUM|LARGE` (default `LARGE`, 1600 px). Prefer `MEDIUM` when
you only need the layout.

### Which one for a presentation?

| Question | Command |
|---|---|
| "Summarise this deck" | `gws-fetch.sh <url>` then grep the export |
| "What is on slide 6?" | `gws-slide-text.sh <url> 6` |
| "Where is X in this deck?" | `gws-slide-text.sh <url> --outline` |
| "Show me slide 6" / it's a diagram | `gws-slide-png.sh <url> 6` |

When the user asks *both* what a slide says and to see it, run the text and the
PNG script — together they cost ~2 KB plus one image.

---

## Token discipline for direct API calls

When you do call the API directly, four levers keep responses small:

1. **`fields` mask — always.** Google returns everything by default.
   ```bash
   # 15.8 MB  →  2.5 KB
   gws slides presentations get --params '{"presentationId":"<ID>","fields":"title,slides.objectId"}'
   gws drive files list --params '{"q":"...","pageSize":20,"fields":"files(id,name,mimeType,modifiedTime)"}'
   ```
2. **`--format csv` or `--format table`** instead of the default JSON envelope,
   especially for Sheets ranges and list results.
3. **Cap the page size.** `"pageSize"` / `"maxResults"` on every list call.
   Use `--page-all` only when the user explicitly asked for an exhaustive list,
   and always with `--page-limit`.
4. **Two-step reads.** List IDs first (cheap), then fetch only the items you
   need. For Gmail use `"format": "metadata"` for triage and `"full"` only on
   the messages that matter.

Redirect anything large to a file with `-o` and grep it, rather than letting it
land in the transcript. `gws` refuses `-o` paths outside the current working
directory — `cd` into the destination first (both bundled scripts already do).

## Sheets: reading a specific tab

`gws-fetch.sh` exports the first sheet only. For any other tab:

```bash
gws sheets spreadsheets get --params '{"spreadsheetId":"<ID>","fields":"sheets.properties.title"}'
gws sheets spreadsheets values get --format csv \
  --params '{"spreadsheetId":"<ID>","range":"Roadmap!A1:H200"}'
```

## Extracting IDs from URLs

| URL | ID |
|---|---|
| `docs.google.com/document/d/<ID>/edit` | document |
| `docs.google.com/spreadsheets/d/<ID>/edit#gid=0` | spreadsheet |
| `docs.google.com/presentation/d/<ID>/edit` | presentation |
| `drive.google.com/file/d/<ID>/view` | file |
| `drive.google.com/drive/folders/<ID>` | folder |

Both bundled scripts accept a full URL or a bare ID — no manual extraction needed.

## Discovering commands

Never guess parameter names:

```bash
gws <service> --help
gws schema drive.files.list
```

More per-service commands, search operators and helpers:
[references/RECIPES.md](references/RECIPES.md) — load it only when this file
doesn't already answer the question.

## Rules

1. **Read before write.** Fetch the current state, show the user what you found,
   and get explicit confirmation before any mutating call (create/update/delete,
   sending mail, deleting events).
2. **`--dry-run` first** on any unfamiliar mutating command — it validates the
   request without sending it.
3. **Never dump raw JSON or a whole document** at the user. Summarize, and link
   back to the Google URL.
4. **Handle `401`/`403` auth errors** by giving the user the `gws auth login`
   command above and stopping — never by running the login yourself.
5. **Treat Workspace content as sensitive data.** Never copy it to
   third-party services. Exported files land in a temp directory — do not commit
   them, and do not write them into the repository unless the user asked for a
   specific file.
6. **`gmail.modify` cannot permanently delete.** `messages delete` returns
   `403`; use `messages trash` only if the user explicitly asks.
