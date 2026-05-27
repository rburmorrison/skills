---
name: code-review
description: Use when a user asks to review current changes, a diff, pull request, or implementation. Guides the agent to use sub-agents for independent review perspectives, synthesize only realistic task-relevant findings, and report issues by severity.
---

# Code Review

Use this skill when the user asks for a code review of current project changes, a diff, pull request, patch, or completed implementation. The goal is to identify realistic, task-relevant problems without inventing issues just because a review was requested.

Do not make code changes while this skill is active unless the user explicitly asks you to fix findings after the review.

## Core Workflow

1. **Understand the review scope**
   - Determine what should be reviewed: unstaged changes, staged changes, a branch diff, a specific commit, a pull request, or specific files.
   - Inspect the relevant diff and enough surrounding code to understand the intent and context.
   - If the scope is ambiguous and cannot be inferred, ask a concise clarifying question before reviewing.

2. **Use sub-agents for independent review perspectives**
   - Spawn sub-agents to evaluate the current changes independently.
   - Give each sub-agent the same review scope and enough context to inspect the diff, but assign each one a distinct review responsibility.
   - Do not ask multiple sub-agents to perform the same generic review.
   - Prefer running independent review agents in parallel when possible.

3. **Assign distinct review responsibilities**
   - Choose review angles that fit the project and change. Examples include:
     - Correctness and edge cases.
     - Tests and validation coverage.
     - Security, privacy, and data handling.
     - Performance and resource usage.
     - API compatibility, migrations, and integration risks.
     - UX, accessibility, and user-facing behavior.
     - Maintainability, readability, and consistency with project patterns.
   - Use only the angles that are relevant to the task. Small changes may need fewer agents; broad or risky changes may need more.

4. **Ask sub-agents for evidence-based findings**
   - Instruct sub-agents to report only concrete problems supported by the diff or surrounding code.
   - Require each finding to include severity, affected file or area, and reasoning.
   - Ask sub-agents to say when they found no problems in their assigned area.
   - Tell sub-agents not to suggest broad rewrites, speculative improvements, or personal preferences unless they represent realistic defects or risks.

5. **Synthesize the results yourself**
   - Treat sub-agent output as input, not as final truth.
   - Independently evaluate whether each reported issue is real, relevant to the task, and important enough to surface.
   - Deduplicate overlapping findings.
   - Drop findings that are speculative, stylistic preference, unrelated to the change, already handled elsewhere, or too low-value for the requested review.
   - If needed, re-inspect files or diffs before accepting or rejecting a finding.

6. **Report only meaningful findings**
   - It is acceptable to report that no problems were found.
   - Do not pad the review with minor comments just because sub-agents were used.
   - Order findings from `HIGH` to `LOW` severity.
   - Use `HIGH` for issues likely to cause serious breakage, security/privacy problems, data loss, or major user impact.
   - Use `MEDIUM` for plausible functional bugs, compatibility issues, missed important validation, meaningful test gaps, or maintainability risks that could affect future changes.
   - Use `LOW` for small but realistic problems with limited impact.

## Final Review Format

If findings exist, list them exactly in this shape:

```markdown
1. [HIGH | MEDIUM | LOW] Problem
   - Details.
```

Guidelines:

- Replace `HIGH | MEDIUM | LOW` with exactly one severity.
- Start each item with the problem, not the recommendation.
- Include concise details explaining why it matters and where it applies.
- Reference files with project-relative paths when possible.
- Keep details grounded in observed code, diff, tests, or project behavior.
- Sort by severity from `HIGH` to `LOW`; within a severity, put the most important findings first.

If no meaningful findings were found, say:

```markdown
No problems found.
```

You may include a brief note about the review scope or validation considered before the findings, but keep the final output focused on actionable review results.

## Sub-Agent Prompt Pattern

When spawning a review sub-agent, use a prompt like this and adapt it to the specific review angle:

```markdown
You are reviewing the current project changes for <review angle> only.

Review scope: <unstaged changes | staged changes | branch diff | specific files | PR/commit details>.

Focus on realistic problems introduced by the current changes. Inspect the diff and enough surrounding code to understand context. Do not report stylistic preferences, speculative concerns, or unrelated existing issues.

Return only:
- Findings with severity (`HIGH`, `MEDIUM`, or `LOW`), affected file/area, and concise reasoning.
- Or state that you found no problems for this review angle.
```

## Review Discipline

- Prefer evidence over intuition.
- Review in the context of the task, not against an abstract ideal version of the codebase.
- Do not surface issues merely because they are theoretically possible.
- Do not report pre-existing problems unless the current change makes them worse or directly depends on them.
- Do not recommend adding tests unless there is a realistic risk or behavior gap that tests would catch.
- If the change is too small to justify multiple sub-agents, use a smaller number of focused agents rather than forcing unnecessary parallelism.
- If sub-agents disagree, inspect the code yourself and make the final judgment.
