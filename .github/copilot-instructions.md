# Copilot Instructions — Vault Tech Logs

This repository is a **Markdown-only** daily work log.

## Hard Rules (Non-Negotiable)

- Do not add code, scripts, extensions, automations, or tooling to this repo.
- Do not create or modify Markdown files under `assets/` (images-only).
- Do not modify files outside the scope described below.

If the user requests something that cannot be completed purely by editing Markdown via Copilot Chat, respond with exactly:

sorry, copilot cannot complete this task - limitation #1

## Where Content Lives

- Daily entries: `entries/YYYY-MM-DD.md`
- Images: `assets/YYYY-MM-DD/*`
- System spec: `docs/task-spec.md`
- Current category standard: `templates/template.md`

## Default Behavior

When the user provides task updates:

1. Determine today’s date and target file `entries/YYYY-MM-DD.md`.
2. If today’s file does not exist, create it containing the date header plus the full commented category skeleton (per spec/template).
3. Read today’s file (and optionally the most recent few entry files for context) but **only edit today’s file**.
4. Apply updates with minimal diffs.

## Parsing User Updates

- If the user provides multiple tasks (bullets, numbers, or plain newline-separated items), create one task per item.
- Separate tasks with exactly one empty line (per `docs/task-spec.md`).
- Do not indent task lines.

## Formatting + Consistency

- Treat `docs/task-spec.md` as the single source of truth.
- Treat `templates/template.md` as the canonical category list and ordering.
- Categories are hidden unless they contain tasks:
  - Active: `## 🛠️ Working On` (preceded by a `<br>` and an empty line)
  - Hidden: `<!-- 🛠️ Working On -->`
- Insert a single line containing exactly `<br>` followed by an empty line immediately above each active category header.
- Do not add `<br>` lines for commented categories.

## Tickets and Tags

- Convert Jira keys `PROJECTKEY-1234` into ticket links using `https://yourcompany.atlassian.net/browse/` in the Markdown link format `[KEY](url)`.
- If the user provides a Jira browse URL like `https://yourcompany.atlassian.net/browse/PROJECTKEY-1234`, normalize it to `[PROJECTKEY-1234](https://yourcompany.atlassian.net/browse/PROJECTKEY-1234)`.
- Never use the raw-URL-in-brackets form (forbidden): `[https://yourcompany.atlassian.net/browse/PROJECTKEY-1234]`.
- If no ticket exists in a task, add `[MISSING_TICKET]`.
- Tags are limited to date tags (`[Due YYYY-MM-DD]`, `[Reminder YYYY-MM-DD]`, `[Completed YYYY-MM-DD]`), the Jira ticket link, and `[MISSING_TICKET]` when no Jira key exists.
- Enforce tag ordering **only among tags present**: Due > Reminder > Completed > Ticket link (or `[MISSING_TICKET]` when no ticket exists).
- Never invent or prepend `Due`/`Reminder`/`Completed`; only use bracketed date tags when the user explicitly provided the date.
- Place tags at the start of the task line.
