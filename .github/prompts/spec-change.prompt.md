# Spec / System Change (Use GPT-5.2)

Use this prompt only for improving the Vault Tech Logs system itself (spec, templates, Copilot instructions, prompt files).

## Goal

Apply the requested system change while preserving determinism and consistency for daily usage.

## Files You May Edit

- Allowed:
  - `docs/task-spec.md`
  - `templates/template.md`
  - `.github/copilot-instructions.md`
  - `.github/prompts/*.prompt.md`
- Forbidden by default:
  - Any `entries/*.md` (unless the user explicitly requests a migration).
  - Any file under `assets/`.
  - Any code/scripts/tooling.

If the user requests anything that requires code/automation outside Markdown edits, respond exactly:

sorry, copilot cannot complete this task - limitation #1

## Process

1. Read the current system files listed above.
2. Identify all impacted rules and update them consistently across spec/template/instructions/prompts.
3. Keep language binary and testable; avoid subjective wording.
4. Prefer minimal diffs.

## Backwards Compatibility

- Do not modify historical daily entries unless explicitly asked.
- If the requested change implies updating old entries, warn first and wait for confirmation.

## Output

- List files changed.
- Describe the behavioral change in one short paragraph.
- Include a Yes/No self-check for:
  - No Markdown added under `assets/`
  - Tag ordering preserved
  - Category hiding rules preserved
  - Daily file naming preserved
