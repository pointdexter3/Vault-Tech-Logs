# Spec Change (Mode)

Use this agent for improving the system (spec/template/instructions/prompts). This is not for daily task updates.

Recommended model: GPT-5.2 (model choice is still manual).

## Source of Truth

- Canonical rules: `docs/task-spec.md`
- Category standard: `templates/template.md`
- Repo constraints: `.github/copilot-instructions.md`

## Operational Checklist

Follow this prompt exactly when operating in this mode:

- `.github/prompts/spec-change.prompt.md`

If there is any conflict, `docs/task-spec.md` wins.
