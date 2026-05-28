---
name: gitmoji-commits
description: Write or propose concise Git commit messages using the Gitmoji convention. Use when the user asks for a commit message, Gitmoji commit, help choosing a Gitmoji, or committing changes; prefer shortcodes, omit scope specifications, and propose commits before making them.
---

# Gitmoji Commits

Use this skill when the user asks you to write, revise, or choose a Gitmoji commit message for staged changes, unstaged changes, a diff, or a described change.

## Output Contract

There are two distinct output modes. Choose the mode from the user's request and follow it exactly:

1. **Commit message only**: When the user asks only for a commit message, return only the commit message unless they explicitly ask for explanation or alternatives.
2. **Commit proposal**: When the user asks you to make commits, do not output only the commit message. Do not commit immediately. First write all proposed commits to the user using the full surrounding text and file list formats in [Commit Proposals](#commit-proposals), then wait for explicit approval before making any commits.

The commit proposal format is mandatory. Even if other instructions say to return only the commit message, that applies only to commit-message-only requests and must not override the proposal format when the user asks you to commit changes.

Use this subject format:

```text
:<gitmoji_shortcode>: <Imperative summary>
```

Rules:

- Use exactly one Gitmoji shortcode, not the Unicode emoji.
- Do not include a scope specification. Avoid formats like `:sparkles: (api): Add endpoint`.
- Choose the shortcode based on the primary intent of the change, not every file touched.
- Write the summary in imperative mood, capitalized after the shortcode.
- Keep the subject concise; target about 50 characters when practical.
- Do not end the subject line with punctuation.
- Include a body only when it adds useful context not clear from the subject.
- If using a body, separate it from the subject with one blank line and wrap body lines at 72 characters.
- When making commits, split changes into multiple commits when the work can be distinctly separated by file and purpose.
- Before making any commits, show every proposed commit and the files it will include, then wait for the user to approve.

## Workflow

1. If a diff or change description is provided, use it directly.
2. If the user asks for a commit message without providing changes, inspect the repository state when tools are available:
   - Prefer staged changes with `git --no-pager diff --staged`.
   - If nothing is staged, inspect `git --no-pager diff` and `git --no-pager status --short`.
   - Do not run commands that modify the repository.
3. Identify the primary purpose of the change.
4. If the user asked you to make commits, group changed files into one or more commits:
   - Use multiple commits when the work can be distinctly split by file and purpose.
   - Use a single commit when the changes are tightly related or cannot be cleanly separated by file.
   - Do not split a file across commits unless the user explicitly asks for partial staging.
5. Select the closest Gitmoji shortcode for each proposed commit from the reference below.
6. If the user asked only for a commit message, return the final commit message only.
7. If the user asked you to make commits, show the complete commit proposal first using the required format below and wait for explicit approval before running any committing commands. Do not reduce the proposal to a bare `:shortcode: Message` line.

If multiple shortcodes could apply, prefer the one that best describes the main purpose. For example, a bug fix that also updates tests should use `:bug:`, not `:white_check_mark:`. Use `:white_check_mark:` only when the primary purpose is changing tests.

## Official Format Preference

The Gitmoji specification allows both Unicode and shortcode intentions, and it allows an optional scope:

```text
<intention> [scope?][:?] <message>
```

For this user's preferred style, always use the shortcode intention and omit scope specifications.

## Commit Proposals

When the user asks you to commit changes, always propose the commit or commits before making them. This section defines the exact user-facing output required before approval.

Do not omit the introductory sentence, bullet list, file list, or closing approval prompt. The response must include the surrounding text shown below, not just the commit subject.

Use this format for multiple commits:

```text
I would like to make the following commits:

- :shortcode1: Message 1
  - file1.md
  - file2.md
- :shortcode2: Message 2
  - file3.md

Let me know if you'd like me to commit these changes.
```

Use this format for a single commit:

```text
I would like to make the following commit:

- :shortcode: Message
  - file1.md
  - file2.md
  - file3.md

Let me know if you'd like me to commit these changes.
```

After approval, make only the approved commits. If the user requests changes to the plan, revise and present the proposal again before committing.

## Gitmoji Shortcode Reference

| Shortcode | Primary purpose |
| --- | --- |
| `:art:` | Improve code structure or formatting |
| `:zap:` | Improve performance |
| `:fire:` | Remove code or files |
| `:bug:` | Fix a bug |
| `:ambulance:` | Apply a critical hotfix |
| `:sparkles:` | Introduce features |
| `:memo:` | Add or update documentation |
| `:rocket:` | Deploy changes |
| `:lipstick:` | Add or update UI and style files |
| `:tada:` | Begin a project |
| `:white_check_mark:` | Add, update, or pass tests |
| `:lock:` | Fix security or privacy issues |
| `:closed_lock_with_key:` | Add or update secrets |
| `:bookmark:` | Create release or version tags |
| `:rotating_light:` | Fix compiler or linter warnings |
| `:construction:` | Mark work in progress |
| `:green_heart:` | Fix CI builds |
| `:arrow_down:` | Downgrade dependencies |
| `:arrow_up:` | Upgrade dependencies |
| `:pushpin:` | Pin dependencies to specific versions |
| `:construction_worker:` | Add or update CI build system |
| `:chart_with_upwards_trend:` | Add or update analytics or tracking code |
| `:recycle:` | Refactor code |
| `:heavy_plus_sign:` | Add a dependency |
| `:heavy_minus_sign:` | Remove a dependency |
| `:wrench:` | Add or update configuration files |
| `:hammer:` | Add or update development scripts |
| `:globe_with_meridians:` | Internationalization and localization |
| `:pencil2:` | Fix typos |
| `:poop:` | Write bad code that needs improvement |
| `:rewind:` | Revert changes |
| `:twisted_rightwards_arrows:` | Merge branches |
| `:package:` | Add or update compiled files or packages |
| `:alien:` | Update code due to external API changes |
| `:truck:` | Move or rename resources |
| `:page_facing_up:` | Add or update license |
| `:boom:` | Introduce breaking changes |
| `:bento:` | Add or update assets |
| `:wheelchair:` | Improve accessibility |
| `:bulb:` | Add or update source-code comments |
| `:beers:` | Write deliberately rough or playful code |
| `:speech_balloon:` | Add or update text and literals |
| `:card_file_box:` | Perform database-related changes |
| `:loud_sound:` | Add or update logs |
| `:mute:` | Remove logs |
| `:busts_in_silhouette:` | Add or update contributors |
| `:children_crossing:` | Improve user experience or usability |
| `:building_construction:` | Make architectural changes |
| `:iphone:` | Work on responsive design |
| `:clown_face:` | Add or update mocks |
| `:egg:` | Add or update an easter egg |
| `:see_no_evil:` | Add or update `.gitignore` |
| `:camera_flash:` | Add or update snapshots |
| `:alembic:` | Perform experiments |
| `:mag:` | Improve SEO |
| `:label:` | Add or update types |
| `:seedling:` | Add or update seed files |
| `:triangular_flag_on_post:` | Add, update, or remove feature flags |
| `:goal_net:` | Catch errors |
| `:dizzy:` | Add or update animations and transitions |
| `:wastebasket:` | Deprecate code that needs cleanup |
| `:passport_control:` | Work on authorization, roles, or permissions |
| `:adhesive_bandage:` | Apply a simple non-critical fix |
| `:monocle_face:` | Explore or inspect data |
| `:coffin:` | Remove dead code |
| `:test_tube:` | Add a failing test |
| `:necktie:` | Add or update business logic |
| `:stethoscope:` | Add or update health checks |
| `:bricks:` | Change infrastructure |
| `:technologist:` | Improve developer experience |
| `:money_with_wings:` | Add sponsorship or money-related infrastructure |
| `:thread:` | Add or update multithreading or concurrency code |
| `:safety_vest:` | Add or update validation code |
| `:airplane:` | Improve offline support |
| `:t-rex:` | Add backward compatibility |

## Examples

Good:

```text
:bug: Fix stale session refresh
```

```text
:sparkles: Add saved search filters
```

```text
:memo: Document release workflow
```

Avoid:

```text
🐛 Fix stale session refresh
```

```text
:sparkles: (search): Add saved filters
```
