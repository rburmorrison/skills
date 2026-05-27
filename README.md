# Personal Skills

My personal collection of agent skills. Each skill lives in `skills/<name>/` and is defined by a `SKILL.md` file.

## Skills

- `planning`: Guides feature, refactor, bug-fix, and implementation planning before code changes begin.
- `feature-stubbing`: Stubs planned features by designing caller-facing data structures and public functions or methods first, using idiomatic placeholder bodies.
- `code-review`: Reviews diffs, pull requests, and implementations with a focus on realistic bugs, risks, regressions, and missing validation.
- `gitmoji-commits`: Writes concise Gitmoji-style commit messages and commit proposals.

## Install

Install all skills from this repository with the Skills CLI:

```sh
npx skills add rburmorrison/skills
```

Install one skill by name:

```sh
npx skills add rburmorrison/skills --skill planning
npx skills add rburmorrison/skills --skill feature-stubbing
npx skills add rburmorrison/skills --skill code-review
npx skills add rburmorrison/skills --skill gitmoji-commits
```

You can also install directly from the Git URL:

```sh
npx skills add git@github.com:rburmorrison/skills.git
```

Or install a specific skill globally:

```sh
npx skills add git@github.com:rburmorrison/skills.git --skill planning --global
npx skills add git@github.com:rburmorrison/skills.git --skill feature-stubbing --global
npx skills add git@github.com:rburmorrison/skills.git --skill code-review --global
npx skills add git@github.com:rburmorrison/skills.git --skill gitmoji-commits --global
```
