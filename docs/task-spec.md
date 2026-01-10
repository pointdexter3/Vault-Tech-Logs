# Vault Tech Logs — Task Spec

This document defines the **single source of truth** for how daily task logs are created and updated in this repo.

## Hard Constraints

- This repo is **Markdown-only** for daily logs.
- Do **not** add code, scripts, extensions, automations, or non-Markdown tooling here.
- The `assets/` folder is **images-only**. Never create Markdown files under `assets/`.
- If the user requests something that cannot be completed purely by editing Markdown via Copilot Chat, respond with exactly:

sorry, copilot cannot complete this task - limitation #1

## Daily File Location

- Exactly one daily file per day.
- Daily entry path format:
  - `entries/YYYY-MM-DD.md`
  - Example: `entries/2026-01-10.md`

## Daily File Header

- The first line of every daily file must be a Markdown H1 with the date in **MMM d, yyyy** format.
  - Example: `# January 10, 2026`
- New daily files must start with the header and then include the full category skeleton (all categories commented out), so:
  - VS Code Markdown Preview shows only categories that contain tasks.
  - manual editing is easy because all categories are present.
- If a daily file already exists and is missing the header, insert the header above the existing content.

## Images

- Store pasted images at the repo root:
  - `assets/YYYY-MM-DD/<filename>`
- From a daily file under `entries/`, link images using:
  - `../assets/YYYY-MM-DD/<filename>`
- Do not “fix”, rename, move, or delete images/links unless explicitly asked.

## Categories

- Categories are defined by the current standard in `templates/template.md`.
- Categories may change over time.
  - Do not update old daily files to match new categories unless the user explicitly requests it.
  - If asked to update old daily files, warn before making changes.

### Category Header Formatting

- A category header is a single line with an emoji prefix, exactly matching the template’s category name.
  - Example: `🛠️ Working On`
- **Three empty lines** must appear immediately above each category header line.
- Category order in a daily file must follow the order in `templates/template.md`.

### Hidden / Commented Categories

- Categories must be **hidden** unless they contain at least one task.
- Hidden categories are represented as an HTML comment containing the category header text:
  - Example: `<!-- 🛠️ Working On -->`
- Behavior rules:
  - When adding the first task to a category, ensure that category header is **uncommented**.
  - When moving/removing tasks so a category becomes empty, the category header must become **commented**.
  - Daily files must contain the full category skeleton; unused categories remain commented.

### Category Skeleton Requirement

- After the date header, include every category from `templates/template.md` as a commented header line.
- Maintain category order exactly as in `templates/template.md`.
- Ensure **three empty lines** immediately above each commented category line.

## Tasks (Category Items)

“Task”, “item”, and “category item” refer to the same thing.

### Task Formatting Rules

- Tasks are **not** list items.
  - Do not prefix tasks with `-`, `*`, `1.`, etc.
- Each task must belong to exactly one category.
- Separate tasks with **one empty line**.
- If the user provides multiple tasks in a list format, convert each list entry into its own task paragraph, separated by one empty line.
- Tasks may contain internal formatting (including lists) **only** if the user included those details inside the task.

## Tickets, Links, and Tags

### Jira Ticket Links

- Detect Jira ticket keys in the format `PROJECTKEY-1234` (e.g., `BDBN-0001`).
- Convert every detected ticket key to a Markdown link using the base URL:
  - `https://yourcompany.atlassian.net/browse/`
  - Example: `BDBN-0001` → `[BDBN-0001](https://yourcompany.atlassian.net/browse/BDBN-0001)`

### Ticket Requirement

- Tickets are **not** mandatory.
- If a task contains no Jira ticket key, add the tag `[MISSING_TICKET]`.

### Tag Types

Tags include:
- Due dates: `[Due YYYY-MM-DD]`
- Reminder dates: `[Reminder YYYY-MM-DD]`
- Completed dates: `[Completed YYYY-MM-DD]`
- Ticket links (as described above)
- Other bracket tags: `[Some Tag]`

### Tag Ordering (Strict)

Within a task, enforce this exact tag ordering:

1. Due
2. Reminder
3. Completed
4. Ticket link
5. Other tags (including `[MISSING_TICKET]`)

### Tag Placement (Deterministic)

- Place tags at the **end of the first line** of the task, separated by single spaces.
- Do not reorder the non-tag text of the task.

## Update Policy

- Default behavior: only create/update **today’s** daily file.
- Do not edit older daily files unless explicitly requested.
- Prefer minimal diffs: change only what is required to apply the user’s update and maintain this spec.
