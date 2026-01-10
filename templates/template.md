# Vault Tech Logs — Current Category Standard

This file defines the current category set and their emoji prefixes.

Rules:
- In daily entries, categories must follow the order listed below.
- Categories are hidden unless they contain tasks (comments do not render in preview).
- Hidden category format (HTML comment): `<!-- <emoji> <Category Name> -->`
- Active category format (heading line): `## <emoji> <Category Name>`
- Each active category header must be preceded by a single line containing exactly `<br>` followed by an empty line.

## Categories (in order)

- 🛠️ Working On
- 📚 Learnings
- ✅ Completed
- ⏭️ Next Up
- ⛔ Blockers
- 🧪 Spikes
- ⚙ Vault Tech Enhancements (system improvements only)
- ⚙ Vault Tech Enhancements (system improvements to this repo/system only)
- 👤 FTE
- 💬 Communication
- 📅 Meetings
- 🔁 Follow-ups

## Examples

### New Daily File (no tasks yet)

A new daily file contains the date header and a full commented category skeleton (so you can quickly add tasks manually, while preview stays clean):

# January 10, 2026

<!-- 🛠️ Working On -->



<!-- 📚 Learnings -->



<!-- ✅ Completed -->



<!-- ⏭️ Next Up -->



<!-- ⛔ Blockers -->



<!-- 🧪 Spikes -->



<!-- ⚙ Vault Tech Enhancements (system improvements only) -->



<!-- ⚙ Vault Tech Enhancements (system improvements to this repo/system only) -->



<!-- 👤 FTE -->



<!-- 💬 Communication -->



<!-- 📅 Meetings -->



<!-- 🔁 Follow-ups -->

### Daily File With Tasks (only used categories appear)

# January 10, 2026

<br>

## 🛠️ Working On

[MISSING_TICKET] Finish investigation of XYZ root cause.

[BDBN-0001](https://yourcompany.atlassian.net/browse/BDBN-0001) Implement Japan field mapping changes.




<!-- ✅ Completed -->




<br>

## ⛔ Blockers
[Reminder 2026-01-11] [MISSING_TICKET] Waiting on access approval from IT.

Notes:
- Tags are limited to `[Due YYYY-MM-DD]`, `[Reminder YYYY-MM-DD]`, `[Completed YYYY-MM-DD]`, the Jira ticket link, and `[MISSING_TICKET]` when no ticket exists.
