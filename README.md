# Personal Skills

My personal collection of agent skills. Each skill lives in `skills/<name>/` and is defined by a `SKILL.md` file.

## Skills

- `planning`: Guides feature, refactor, bug-fix, and implementation planning before code changes begin.
- `feature-stubbing`: Stubs planned features by designing caller-facing data structures and public functions or methods first, using idiomatic placeholder bodies.
- `code-review`: Reviews diffs, pull requests, and implementations with a focus on realistic bugs, risks, regressions, and missing validation.
- `gitmoji-commits`: Writes concise Gitmoji-style commit messages and commit proposals.

## Install

Install all skills globally from this repository with the Skills CLI:

```sh
npx skills add rburmorrison/agent-skills --global
```

Omit `--global` from any command to install skills for the current project instead.

Install one skill globally by name:

```sh
npx skills add rburmorrison/agent-skills --skill planning --global
npx skills add rburmorrison/agent-skills --skill feature-stubbing --global
npx skills add rburmorrison/agent-skills --skill code-review --global
npx skills add rburmorrison/agent-skills --skill gitmoji-commits --global
```

