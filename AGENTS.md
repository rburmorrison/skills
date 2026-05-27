# AGENTS.md

This repository contains personal agent skills. Each skill should live in `skills/<name>/` with a `SKILL.md` file.

## Skill Changes

- Keep each skill focused on one reusable workflow or capability.
- Use the skill directory name under `skills/` as the stable install name.
- Keep `SKILL.md` front matter accurate, especially `name` and `description`.
- Prefer concise instructions that an agent can apply directly.

## Documentation

Update `README.md` when a skill is added, removed, or renamed.

Also update `README.md` when a skill is modified in a way that changes its purpose, activation criteria, install name, or user-facing behavior enough to make the existing summary inaccurate.

## Validation

Before finishing changes, check that:

- Every directory under `skills/` has a `SKILL.md`.
- Every listed README skill maps to an existing `skills/<name>/` directory.
- Install examples still use the current repository path and skill names.
