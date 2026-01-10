# Daily Task Update (Free Model)

You are updating a Vault Tech Logs daily entry.

## Goal

Apply the user’s task update to **today’s** daily file with strict formatting and minimal diffs.

## Files You May Edit

- Allowed: `entries/YYYY-MM-DD.md` for today only.
- Forbidden:
  - Any file under `assets/` (images-only).
  - Any other `entries/*.md` unless the user explicitly requests updating an older date.
  - Any non-Markdown files.

If the user requests anything outside these constraints, respond exactly:

sorry, copilot cannot complete this task - limitation #1

## Pre-Read (Context)

1. Read today’s daily file if it exists.
2. Optionally read the most recent 3–7 daily files for context/deduping only (do not edit them).
3. Read `docs/task-spec.md` and follow it strictly.
4. Read `templates/template.md` for category names and ordering.

## Create-or-Update

- If today’s file does not exist, create it with only the date header:
- If today’s file does not exist, create it with:
  - the date header: `# MMMM d, yyyy`
  - the full category skeleton (all categories present as commented headers in the order from `templates/template.md`)
- If today’s file exists but is missing the header, insert the header above existing content.

## Category Rules

- Place tasks under exactly one category.
- Categories must appear in the exact order defined in `templates/template.md`.
- Categories are hidden unless they contain tasks:
  - Hidden: `<!-- <emoji> <Category Name> -->`
  - Active: `## <emoji> <Category Name>`
- Insert a single line containing exactly `<br>` followed by an empty line immediately above each active category header.
- Do not add `<br>` lines for commented categories.
- Always keep the full category skeleton in the daily file:
  - Categories with tasks are active (uncommented).
  - Categories without tasks remain commented.
- If moving tasks causes a category to become empty, convert its header to the commented form.

## Task Rules

- Tasks are paragraphs, not list items.
- Separate tasks with one empty line.
- If user provides multiple tasks in a list, convert each list entry into its own task paragraph.
- Preserve user-provided internal sublists inside the task text.

## Tickets + Tags

- Convert all Jira keys `PROJECTKEY-1234` to ticket links:
  - `[KEY-123](https://yourcompany.atlassian.net/browse/KEY-123)`
- If a task has no Jira key, add `[MISSING_TICKET]`.
- Enforce tag order within each task:
  1) Due, 2) Reminder, 3) Completed, 4) Ticket link, 5) other tags (including `[MISSING_TICKET]`).
- Tags are optional; do not add tags the user did not provide, except `[MISSING_TICKET]` when no Jira key is present.
- Never insert bare `Due` / `Reminder` / `Completed` prefixes.
  - Only add a due tag if the user explicitly provided a due date, and it must be formatted exactly as `[Due YYYY-MM-DD]`.
  - Only add a reminder tag if the user explicitly provided a reminder date, and it must be formatted exactly as `[Reminder YYYY-MM-DD]`.
  - Only add a completed tag if the user explicitly provided a completed date, and it must be formatted exactly as `[Completed YYYY-MM-DD]`.
- Place tags at the start of the first line of the task, separated by single spaces.

## Output

After updating the file:
- State the file you edited.
- State how many tasks you added/moved/completed.
- List the categories you touched.
- Confirm you did not edit anything under `assets/`.
