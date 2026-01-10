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

## Formatting + Consistency

- Treat `docs/task-spec.md` as the single source of truth.
- Treat `templates/template.md` as the canonical category list and ordering.
- Categories are hidden unless they contain tasks:
  - Active: `🛠️ Working On`
  - Hidden: `<!-- 🛠️ Working On -->`
- Three empty lines must appear above each category header/comment.

## Tickets and Tags

- Convert Jira keys `PROJECTKEY-1234` into ticket links using `https://yourcompany.atlassian.net/browse/`.
- If no ticket exists in a task, add `[MISSING_TICKET]`.
- Enforce tag ordering: Due > Reminder > Completed > Ticket link > other tags.
