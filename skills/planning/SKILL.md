---
name: planning
description: Use when a user asks to plan a feature, change, refactor, bug fix, or implementation before coding. Guides the agent to explore the codebase, ask numbered clarifying questions with rationale and recommendations, iterate until intent is clear, then produce and revise an implementation plan until the user approves implementation.
---

# Planning a Feature or Change

Use this skill when the user asks to plan a feature, change, refactor, bug fix, migration, or implementation before making code changes. The goal is to clarify intent, understand the existing codebase, and produce an implementation plan that the user explicitly approves before implementation begins.

Do not implement code while this skill is active unless the user clearly gives permission to proceed with implementation.

## Core Workflow

1. **Explore the codebase first**
   - Inspect the files, symbols, tests, docs, configuration, and existing patterns needed to understand the request.
   - Prefer targeted searches and reads over broad, unfocused exploration.
   - Identify likely impacted areas before asking detailed questions.

2. **Ask clarifying questions**
   - Ask as many questions as needed to make the task unambiguous.
   - Put questions under a `## Questions` header so they are easy to find.
   - Number every question so the user can respond easily.
   - Include why the question matters and, when appropriate, a recommended answer or default.
   - Do not ask questions that can be answered confidently from the codebase.

3. **Re-examine as needed**
   - If the user answers questions, asks counter-questions, or reveals new constraints, inspect relevant parts of the project again before drawing conclusions.
   - Update your understanding based on both the code and the user's answers.

4. **Repeat clarification until clear**
   - Continue alternating between questions and targeted project inspection until the requirements, constraints, and expected behavior are clear enough to plan safely.
   - Do not write the plan while important questions remain unanswered. If uncertainty remains, ask another question or state the assumption you intend to confirm before planning.

5. **Write an implementation plan**
   - Produce a clear plan only after the task is sufficiently understood.
   - Choose a layout that fits the size and shape of the change rather than forcing a fixed template.
   - Include at least:
     - A concise summary of the intended change.
     - The files or areas expected to change.
     - Step-by-step implementation tasks or another structure that makes the work sequence clear.
     - Tests, validation, or manual checks to run.
   - Include additional sections when useful, such as data model changes, API changes, migration notes, risks, tradeoffs, or alternatives considered.
   - Use Mermaid diagrams when they improve understanding, especially for data flow, control flow, class diagrams, state machines, or relationships between meaningful data types.

6. **Iterate on the plan**
   - If the user requests changes, asks questions, or challenges assumptions, respond, re-examine code if needed, and update the plan.
   - Repeat planning and revision until the user explicitly approves implementation.

7. **Wait for implementation approval**
   - End planning turns by asking whether the user wants to approve the plan or adjust it.
   - Do not start implementation until the user gives clear permission, such as "implement this", "go ahead", "approved", or equivalent.

## Clarifying Question Format

Use this format when clarifying questions appear:

```markdown
## Questions

1. Question?
   - **Why it Matters**: Explanation of what decision this affects or what risk it reduces.
   - **Recommendation**: Suggested answer, default, or preferred direction based on the codebase and best practices.
```

Guidelines:

- Keep questions specific and actionable.
- Group related questions logically when there are many.
- Prefer fewer high-value questions over a long list of speculative ones, but ask everything necessary for a safe plan.
- If you recommend an option, explain it briefly and ground it in observed codebase patterns when possible.
- If no questions are needed after exploration, state that no clarification appears necessary and proceed to the plan.

## Implementation Plan Guidance

Do not force every plan into the same template. Use headings and structure that make the specific change easy for the user to evaluate.

Every plan must include:

- A summary of the intended change and expected outcome.
- The files or areas expected to change.
- The implementation approach, organized in whatever way best fits the work.
- A `Tests and Validation` section with commands, targeted tests, broader checks, or manual verification steps.
- A closing approval prompt, such as: "Does this plan look right, or would you like changes before implementation?"

Include optional sections only when they add value, such as architecture notes, data model changes, API changes, migration steps, rollout strategy, risks, tradeoffs, or alternatives considered.

Only write the plan after clarification is complete and the task is understood well enough to proceed.

## Mermaid Guidance

Use Mermaid diagrams when they make the plan easier to evaluate. Prefer simple diagrams over decorative ones.

Good candidates:

- Request/response or data processing flows.
- Relationships among domain types, classes, or modules.
- State transitions.
- Before/after architecture comparisons.

Avoid diagrams when the change is small enough that prose is clearer.

Do not use inline HTML in Mermaid diagrams. Do not add custom theme directives. If accent colors help, use the predefined `accent0` through `accent7` classes with `:::` syntax.

## Planning Discipline

- Be explicit about assumptions.
- Separate verified facts from inferences.
- Prefer the smallest plan that satisfies the request.
- Respect existing project conventions and architecture.
- Identify tests and validation before implementation begins.
- Do not over-plan trivial changes; scale the plan to the risk and complexity of the task.
- Do not produce a plan that depends on invented files, symbols, APIs, or behavior. Verify them first.
