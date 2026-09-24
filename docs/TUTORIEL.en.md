---
description: Complete Second Brain tutorial covering installation, setup, daily use, and troubleshooting.
created_date: 2026-09-24
---
# Tutorial — Second Brain with Obsidian and Copilot App

[Version française](TUTORIEL.md)

This folder is a **ready-to-use personal second brain**: a place to capture your thoughts, find
information, and move your projects forward.

You do not need to know how to code, use a terminal, or write Markdown. The system uses two apps
with different roles:
- **Obsidian** is for reading, navigating the vault, and capturing quick notes.
- **GitHub Copilot App** is for understanding, organizing, and editing the folder's contents.

> **The only rule you need to know before starting**
>
> - Manually capture notes **only in `0_Inbox/`**.
> - To organize or edit anything else in the repository, use **Copilot App**.

You will learn the other rules, Copilot App vocabulary, and how sessions work after installation,
when those concepts become useful.

## 1. Install and back up your second brain

Before you start, obtain the following access in this order:

1. **GitHub** access rights through our internal **Identity Access** software.
2. A GitHub account, which you can create using [this link](https://github.com/orgs/dktunited/sso).
3. A **GitHub Copilot** licence, which you can request using [this form](https://idp.decathlon.net/self-service/github-tools/copilot).

You will also need:

4. **Obsidian**, available from [obsidian.md](https://obsidian.md/download).
5. **GitHub Copilot App**, installed from our internal **Workspace One** app. Do not install it from
   the official GitHub website.
6. **Google Drive for desktop**, also installed from **Workspace One**. It is your safety net; see
   section 1.2.

### 1.1 Get a copy of the template

The template is hosted on GitHub. There are two ways to get it, and neither requires coding:

- **The simplest option**: on the template's GitHub page, click the green **Code** button, then
  **Download ZIP**. Extract the archive to get a ready-to-use folder.
- **The more sustainable option**: click **Fork** in the top right to create your own GitHub copy.
  Install [GitHub Desktop](https://desktop.github.com/), then use **Clone repository** to download
  it to your computer. This option lets you receive future template improvements and keep a
  history of your notes.

Rename the folder if you like, for example `Second-Brain`.

### 1.2 Back it up with Google Drive

**This folder will contain your working memory. If it exists in only one place, a disk failure will
erase it entirely.** Google Drive for desktop solves this without changing your habits: the folder
remains a regular folder on your computer, and every change is automatically uploaded to the cloud.

1. Open **Workspace One**, search for **Google Drive for desktop**, and install it from the internal
   app. Then sign in with your Google account.
2. Installation adds a **Google Drive** location to your computer: a drive (often `G:`) on Windows,
   or a `Google Drive` folder in Finder on macOS. Open it, then open **My Drive**.
3. **Move the second-brain folder there**, the copy you downloaded in step 1.1.

Move it **now**, before opening the folder in Obsidian or Copilot App. If you move it later, both
apps will still point to the old location and will no longer see your notes.

### 1.3 Make it available offline — required

By default, Google Drive **does not download** files to your disk: it displays them and downloads
them only when you open them. Obsidian and Copilot App need the files to be physically present.
Without this setting, you may see empty notes or read errors, and the agent will work with files it
cannot open.

1. In the Google Drive location, right-click the second-brain folder.
2. Choose **Offline access** (the wording may vary by version).
3. Select **Available offline**.
4. Wait until the sync icon shows that the folder has finished downloading.

The folder now exists in two places at once: on your disk, where it is fast and usable without an
internet connection, and in Google Drive, where it can be recovered if your computer fails.

> **Use one computer at a time.** Do not work on the same second brain from two computers
> simultaneously: Google Drive may sync both versions and create duplicate files. Close Obsidian
> and Copilot App on the first computer before opening them on the second.

### 1.4 Before continuing

Keep the folder in this location. Obsidian and Copilot App must open **the same copy**, not two
different copies. Write down its path; you will need it in the next steps.

## 2. Install Obsidian and open the vault

1. Install and open Obsidian.
2. Choose **Open folder as vault** (the wording may vary slightly by version).
3. Select your second-brain folder.
4. Make sure the vault's folder tree appears on the left.

You do not need any additional plugins to get started: the template works with Obsidian as
installed. Your Obsidian settings (theme, shortcuts, plugins) stay on your computer and are not
shared with the template. If Obsidian asks whether you trust this vault, accept only if the folder
comes from the expected source.

### What you can do in Obsidian

- read your notes;
- follow links between notes;
- browse folders;
- write a **raw capture in `0_Inbox/` only**.

For any other edit, stop editing in Obsidian and ask Copilot App to make the change.

## 3. Install Copilot App and open the project

1. Open **Workspace One**, search for **GitHub Copilot App**, and install it from the internal app.
   Do not install it from the official GitHub website.
2. Open GitHub Copilot App and sign in with your GitHub account.
3. Open or add a project from the **same local folder** you selected in Obsidian. If the template
   was provided from GitHub, use the app's option to open or retrieve the repository. If it is
   already on your computer, select that existing folder.
4. Open a conversation in this project.
5. In the model selector, choose **GPT-5.6 Luna** and set reasoning to **Medium**. Make this your
   default to avoid unnecessary billing; choose a higher level only for an exceptionally complex
   request.

The `.github/copilot-instructions.md` file tells Copilot App how to work in this second brain
automatically. You normally do not need to read or edit it.

### Quick check

Copy this prompt into Copilot App:

```text
I just opened the second brain.
Briefly explain the role of each folder and remind me of the rule
for manual edits. Point out any placeholders still present in config.md.
```

If the answer describes this folder and its rules, installation is complete.

## 4. Understand Copilot App

You can start using the system without memorizing its vocabulary. These quick references become
useful now that the apps are installed.

### Essential vocabulary

| Term | Simple explanation | In this project |
|---|---|---|
| **Agent** | The assistant that reads files, reasons, and carries out your request. | It follows `.github/copilot-instructions.md` and can organize the vault. |
| **Skill** | A specialized set of instructions, sometimes accompanied by tools. | `.agents/skills/` may contain optional Copilot App skills. |
| **MCP** | A protocol that connects an agent to external tools or sources through specialized servers. | The company's internal MCP framework can be added during SDLC setup. |
| **SDLC** | A framework that integrates AI into the software development life cycle. | Decathlon AI Augmented SDLC is installed and opened in each project according to its official documentation. |
| **Context** | The information available to the agent when it responds. | The current conversation, project instructions, and relevant notes; not necessarily the entire vault. |
| **Session** | A work conversation with a specific goal. | It helps you work on one coherent subject, such as setup or a particular project. |
| **Vault** | The notes folder opened in Obsidian. | Here, it is this template's folder, also opened in Copilot App. |
| **Limit** | A size limit that helps keep files readable and context manageable. | In `config.md` §5, you set the maximum number of lines for certain files; Copilot App warns you when a limit is reached. |

### Agent, skill, and context: an office analogy

- The app is the **desk** where you work.
- The agent is the **colleague** helping you.
- A skill is a **procedure sheet** that colleague can use for a particular task.
- The context consists of the **documents on the desk** and the current conversation.
- The session is the **work meeting** about one subject.

A skill is not a personal note and does not replace the vault. It explains how to perform a
repetitive task or access a tool; enable or install only the skills you need.

### Why not put everything in one session?

A session is not the second brain's permanent memory: the vault's notes and files are. A very long
conversation eventually contains too many subjects and details; some older items may be less
available to the agent. This increases the risk of:

- mixing up two projects or roles;
- applying an old decision to the wrong subject;
- editing the wrong file;
- making responses slower, less clear, and more costly to review.

The practical rule is **one task per session**: avoid doing everything in the same place. Keep each
session focused on one coherent goal.

This makes the context provided to Copilot App more effective: with fewer competing subjects to
distinguish, the agent is less likely to produce irrelevant responses or changes, and therefore to
hallucinate. Shorter sessions also use less context and help manage costs.

- one session for the initial setup;
- one session for each important project;
- one session for a role if the subject is substantial;
- one session for a weekly review or batch Inbox processing.

Do not combine a project question, Inbox sorting, a weekly review, and a change to the system in
one session. Start a new session when you switch tasks or subjects; this helps Copilot App retain
the right context and avoid editing the wrong place.

Keep using the same session for follow-up questions about the same subject. You do not lose the
project rules when you switch sessions: Copilot App can reread `config.md`, the instructions, and
relevant notes.

## 5. Understand the five folders

The filing system follows the **IPCRA** method:

| Folder | What it is for | Example |
|---|---|---|
| `0_Inbox/` | Raw captures that have not been sorted yet | idea, link, quick task |
| `1_Projets/` | Commitments with a goal and an end date | moving house, launching a website |
| `2_Casquettes/` | Ongoing roles you hold | parent, association lead |
| `3_Ressources/` | Reusable information that applies across contexts | glossary, decision, method |
| `4_Archives/` | Completed or inactive content | completed old project |

### How do you decide where something belongs?

- Not sure what to do with it yet? **`0_Inbox/`**.
- Is there an outcome to reach and an end date? **`1_Projets/`**.
- Does it correspond to a role that continues over time? **`2_Casquettes/`**.
- Could it be useful in several contexts? **`3_Ressources/`**.
- Is it completed or inactive? **`4_Archives/`**.

If you are unsure, capture it in `0_Inbox/` and let Copilot App suggest where it belongs.

Two other folders exist, but you do not need to add content to them yourself: `_systeme/` (how
the system works — decision journal and maintenance routines) and `docs/` (this tutorial).
`docs/` is intentionally hidden from Copilot App so it does not clutter the agent's context in
every conversation.

## 6. First-time project setup

Complete these steps in Copilot App, in order. The prompts are ready to copy and paste and express
your intent. The project's configuration defines its working rules, including the rules governing
edits, so you do not need to repeat them. Routing, reading `config.md` and hubs, following the
pattern, frontmatter, updating Quick Registries, and keeping links consistent are handled
automatically.

### Step 1 — Ask Copilot to explain the system

```text
I'm new to this second brain and I'm not a developer.
Explain how it works in simple terms:
1. what I do in Obsidian;
2. what I do in Copilot App;
3. how a note moves from 0_Inbox to its permanent location.
```

### Step 2 — Personalize `config.md`

```text
Help me personalize config.md. Ask me one question at a time
to fill in my first name, role, context, 2 to 4 ongoing roles,
language, tone, naming conventions, limits, sensitive topics,
and the external tools I use.

Use my chosen language for your replies and new notes. Do not rename folders or files,
or translate existing notes, unless I ask.

Do not guess any information or put sensitive data in the file.
After I answer, show me a complete summary of the information collected
and ask for my approval before updating config.md.
```

### Step 3 — Create your first role

Replace the items in square brackets before sending the prompt:

Copilot App automatically reads the relevant hub and
`3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md`. You do not need to ask for this in
the prompt.

```text
Based on config.md, create my first role: "[ROLE NAME]".
It corresponds to [ROLE DESCRIPTION].

Propose the files to create and their planned content, then wait for my approval.
After I approve, create the role.
```

### Step 4 — Install and open the SDLC

1. Install **Decathlon AI Augmented SDLC** by following the
   [official installation tutorial](https://ai-augmented-development.decathlon.net/docs/ai-augmented-sdlc/tutorials/install).
2. To open it in this project, follow the
   [official getting-started tutorial](https://ai-augmented-development.decathlon.net/docs/ai-augmented-sdlc/tutorials/getting-started).

In the canvas, **Setup project environment** is optional and adds substantial weight to the
project. Use it if you want the **BMAD** method; otherwise, you can skip it. You can install
individual MCPs and skills from their tabs to add only what you need.

### Step 5 — Install your first MCP

1. If the canvas is not already open, send `Open ai augmented` in Copilot App.
2. In the **MCP** tab, install **Atlassian — Jira / Confluence**.
3. In a project conversation, announce the installation and say what you want the MCP to do, for
   example:

```text
I installed the Atlassian — Jira / Confluence MCP. Use it for
[USE CASE].
```

This announcement triggers an update to `config.md` §7. If the available information does not
establish the scope of access or actions, Copilot App will ask you to clarify it.

### Step 6 — Create a project (optional)

This step is optional: you can use the second brain without creating a project right away.

```text
Create a project "[PROJECT NAME]" in 1_Projets/.
Goal: [GOAL].
Expected end date or period: [DATE OR PERIOD].

Ask me for any missing information, then create the project.
```

## 7. Everyday use

### 7.1 Capture an idea manually

In Obsidian, create a new note **in `0_Inbox/`**. Give it a simple name, for example
`YYYY-MM-DD-gift-idea.md`, then write down what is on your mind without trying to classify it.

A capture might look like this:

```markdown
---
description: Raw idea to be sorted.
created_date: YYYY-MM-DD
---

# Gift idea

Free text, a link, or the next question.
```

If you do not know how to name or format the capture, simply write it in a note in `0_Inbox/`,
then ask Copilot App to format it.

### 7.2 Ask Copilot App to classify a capture

```text
I added the capture 0_Inbox/YYYY-MM-DD-gift-idea.md.
Read it and suggest:
1. whether it belongs in Project, Role, Resource, or should remain temporarily
   in Inbox;
2. the name and path of the target note;
3. any missing information.
```

To apply the selected classification:

```text
Apply the selected classification to
0_Inbox/YYYY-MM-DD-gift-idea.md.
```

### 7.3 Request an edit

To correct, add to, or reorganize a note that is no longer in Inbox, always use Copilot App:

```text
In the note [NOTE PATH OR NAME], rewrite the section [SECTION NAME]
to make it clearer and shorter.
```

### 7.4 Find information

```text
Find what we decided about [SUBJECT].
Give me the answer.
```

### 7.5 Prepare a next action

```text
Based on the note [PROJECT PATH], give me:
- the current status;
- any blockers;
- the three most useful next actions;
- the questions I need to answer.
```

### 7.6 Archive a completed project

```text
The project [PROJECT NAME] is complete.
Archive it.
```

## 8. Maintain the system

Once a week, run this prompt in Copilot App:

```text
Run the weekly review of my second brain.
```

Once a month, use:

```text
Run the monthly retrospective of my second brain.
```

## 9. Rules to remember

- **Inbox = manual capture.** If in doubt, capture it there.
- **Copilot App = organizing and writing in the repository.** Even a small correction to a project
  or resource must be made through the app.
- **Model and cost: GPT-5.6 Luna + Medium reasoning by default.** Check this setting at the
  beginning of each new session and increase the reasoning level only when the task requires it.
- **Obsidian = reading, navigation, and capture.** Do not directly edit other folders.
- **Copilot App does not automatically reread `4_Archives/`**: explicitly ask to restore an
  archived item.
- Sensitive information listed in `config.md` must never be written to the vault.
- Review Copilot App's summary of changed files before continuing your work.
- **Your backup depends on two conditions** (section 1.2): the folder is in *My Drive* and is
  marked **Available offline**. Check this occasionally — the Google Drive icon in the taskbar
  should indicate that everything is synced.

## 10. Troubleshooting

### Copilot App cannot see my notes

Check that Obsidian and Copilot App are using exactly the same local folder. If you opened a second
copy of the template, close it and reopen the original folder in both apps.

### An edit made in Copilot App does not appear in Obsidian

Ask Obsidian to reload the vault, or close and reopen the vault. Also check that Copilot App has
finished its operation and that its summary shows the correct file path.

### I want to edit a note directly outside Inbox

Do not do this in Obsidian. Copy your request into Copilot App, for example:

```text
Edit the note [PATH] to [GOAL], following the project rules.
```

### I already edited a note manually outside `0_Inbox/`

That happens, and it is okay. The risk is not the edit itself, but that it may cause other things
to become inconsistent: a registry pointing to the wrong place, a broken link, or damaged
frontmatter. Ask Copilot App to check:

```text
I manually edited the note [PATH] outside 0_Inbox.
Check what this edit may have broken: frontmatter, Quick Registry, wikilinks,
and the note's line limit. List the problems and suggest a fix for each.
```

If the note is badly damaged, Google Drive keeps previous versions: right-click the file in Google
Drive, then choose **Manage versions**.

### A note appears empty, or Obsidian says it cannot open it

This is almost always caused by the offline setting being missing (section 1.3). Check that the
second-brain folder is marked **Available offline** in Google Drive, and wait for the download to
finish.

### I see duplicate files with names like "... (1).md"

Two computers worked on the same second brain at the same time. Close Obsidian and Copilot App
everywhere except one computer, then ask Copilot App to clean up:

```text
The vault contains duplicate files created during sync
(names like "... (1).md"). Compare each duplicate with the original
and tell me which one to keep.
```

## 11. Further references

- `config.md` contains your personal preferences and sensitive-topic boundaries.
- `.github/copilot-instructions.md` contains Copilot App's working rules.
- `3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md` explains how to create a new
  branch or note.
- `_systeme/routines.md` describes the weekly review and monthly retrospective.
- `_systeme/_systeme.md` is the entry point for the system folder.
- `.agents/skills/` may contain optional Copilot App skills. They are not required to get started.

The template uses readable Markdown, but you do not need to know its syntax: ask Copilot App to
create or edit notes while following the system's rules.
