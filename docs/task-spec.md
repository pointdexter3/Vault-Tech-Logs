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

- An active (uncommented) category header is a Markdown H2 line with an emoji prefix, exactly matching the template’s category name.
  - Example: `## 🛠️ Working On`
- A single line containing exactly `<br>` followed by an empty line must appear immediately above each active category header line.
  - Rationale: Markdown renderers collapse extra blank lines; `<br>` produces consistent visible spacing.
- Do not add `<br>` lines for commented categories (comments should remain visually hidden in preview).
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
- Do not include `<br>` lines in the skeleton (the skeleton is commented; `<br>` would render and create visible blank space).

## Tasks (Category Items)

“Task”, “item”, and “category item” refer to the same thing.

### Task Formatting Rules

- Tasks are **not** list items.
  - Do not prefix tasks with `-`, `*`, `1.`, etc.
- Do not indent tasks; task text must start at the beginning of the line.
- Each task must belong to exactly one category.
- Separate tasks with **one empty line**.
- If the user provides multiple tasks, create **one task per item** and separate them with one empty line.
  - This includes:
    - Markdown lists (bulleted or numbered)
    - Plain newline-separated items (one task per non-empty line)
    - “Category label” followed by multiple lines (each subsequent non-empty line is its own task)
- Tasks may contain internal formatting (including lists) **only** if the user included those details inside the task.

## Tickets, Links, and Tags

### Jira Ticket Links

- Detect Jira ticket keys in the format `PROJECTKEY-1234` (e.g., `BDBN-0001`).
- Convert every detected ticket key to a Markdown link using the base URL:
  - `https://yourcompany.atlassian.net/browse/`
  - Example: `BDBN-0001` → `[BDBN-0001](https://yourcompany.atlassian.net/browse/BDBN-0001)`
- Also detect Jira browse URLs in the format `https://yourcompany.atlassian.net/browse/PROJECTKEY-1234`.
  - Normalize them to the same Markdown link format:
    - Example: `https://yourcompany.atlassian.net/browse/BDBN-0001` → `[BDBN-0001](https://yourcompany.atlassian.net/browse/BDBN-0001)`
- Never use the raw-URL-in-brackets form:
  - Forbidden: `[https://yourcompany.atlassian.net/browse/BDBN-0001]`

### Ticket Requirement

- Tickets are **not** mandatory.
- If a task contains no Jira ticket key, add the tag `[MISSING_TICKET]`.

### Tag Types

Tags are limited to:
- Due dates: `[Due YYYY-MM-DD]`
- Reminder dates: `[Reminder YYYY-MM-DD]`
- Completed dates: `[Completed YYYY-MM-DD]`
- Ticket links (as described above)
- Ticket placeholder when no Jira key exists: `[MISSING_TICKET]`

### Tag Ordering (Strict)

If a task contains multiple tags, enforce this exact ordering **among the tags present**:

1. Due
2. Reminder
3. Completed
4. Ticket link, or `[MISSING_TICKET]` when no Jira key exists

Notes:
- Date tags include `Due`/`Reminder`/`Completed`. Date tags are optional.
- Never add `[Due ...]`, `[Reminder ...]`, or `[Completed ...]` unless the user explicitly provided the corresponding date.
- Never add a bare `Due`/`Reminder`/`Completed` token; date tags must use the bracketed formats above.

Examples:

`[MISSING_TICKET] Investigate flaky integration test.`

`[Due 2026-01-15] [MISSING_TICKET] Ship v1 rollout checklist.`

### Tag Placement (Deterministic)

- Place tags at the **start of the first line** of the task, separated by single spaces.
- Do not reorder the non-tag text of the task.

## Update Policy

- Default behavior: only create/update **today’s** daily file.
- Do not edit older daily files unless explicitly requested.
- Prefer minimal diffs: change only what is required to apply the user’s update and maintain this spec.
