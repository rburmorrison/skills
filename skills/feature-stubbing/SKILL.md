---
name: feature-stubbing
description: Use when a user wants to stub out a planned feature by designing caller-facing data structures, public functions, methods, modules, traits, classes, or interfaces first, with idiomatic placeholder bodies instead of full implementation.
---

# Feature Stubbing

Use this skill when the user wants to stub out a feature before implementing it. The goal is to design the public interface from the caller's perspective first, then add data structures and public functions, methods, modules, traits, classes, or interfaces with idiomatic placeholder bodies.

This skill is commonly used after an implementation plan has been approved. If no plan exists, first clarify the caller-facing behavior and public contract before editing code.

Do not implement the feature logic while this skill is active unless the user explicitly asks you to move beyond stubbing.

## Core Workflow

1. **Confirm the stubbing scope**
   - Identify the approved plan, feature description, or specific API surface to stub.
   - If the scope is unclear, ask concise clarifying questions before editing.
   - Determine which modules, packages, files, or call sites are likely affected.
   - Keep the work limited to public contract and necessary supporting types.

2. **Start from the caller's perspective**
   - Inspect existing call sites, neighboring APIs, tests, docs, or examples to understand project conventions.
   - If caller usage is not already clear, propose or ask for example usage before choosing signatures.
   - Design names, arguments, return types, errors, async behavior, ownership, mutability, side effects, and visibility around the caller's needs.
   - Prefer the smallest public surface that satisfies the planned feature.

3. **Stub data structures first**
   - Add the public or shared data structures required by the API: structs, classes, records, enums, tagged unions, interfaces, protocols, traits, type aliases, schemas, or equivalent constructs.
   - Include fields, variants, and type parameters implied by the plan or caller usage.
   - Avoid speculative private internals that are not required by the public contract.
   - Match existing naming, serialization, validation, error, and documentation patterns.

4. **Stub public functions and methods**
   - Add signatures with the intended visibility, arguments, return types, generics, trait bounds, exceptions, effects, or async markers.
   - Use idiomatic placeholder bodies rather than real implementation logic.
   - Prefer placeholders that let the project parse, compile, or typecheck when practical.
   - Add doc comments only when they clarify non-obvious contract decisions, preconditions, or intended behavior.

5. **Use idiomatic placeholders**
   - Python:
     ```python
     def my_func(arg1: str) -> None:
         raise NotImplementedError
     ```
   - Rust:
     ```rust
     fn my_func(arg1: &str) {
         todo!();
     }
     ```
   - TypeScript/JavaScript:
     ```ts
     function myFunc(arg1: string): void {
       throw new Error("Not implemented");
     }
     ```
   - Go:
     ```go
     func myFunc(arg1 string) {
         panic("not implemented")
     }
     ```
   - Ruby:
     ```ruby
     def my_func(arg1)
       raise NotImplementedError
     end
     ```
   - For other languages, use the local convention for explicit unimplemented placeholders.

6. **Preserve project conventions**
   - Follow existing module organization, naming, formatting, visibility, typing, error handling, and dependency patterns.
   - Add imports, exports, re-exports, declarations, or registration entries needed for callers to access the stubs.
   - Do not add dependencies unless the public contract truly requires them.
   - Do not rename or reorganize unrelated code.

7. **Handle tests carefully**
   - Do not add tests by default just because stubs were created.
   - Add or update minimal tests, examples, fixtures, or snapshots only when they clarify the public contract, document intended caller behavior, or the user asks for them.
   - If tests exercise placeholder bodies, it is acceptable for them to fail because implementation is intentionally incomplete; report that clearly.

8. **Validate the stubs**
   - Run the most targeted parser, formatter, typecheck, lint, or compile command available for the changed area when practical.
   - Treat syntax errors, type errors in signatures, missing exports, or broken imports as issues to fix.
   - Distinguish expected placeholder failures from accidental validation failures.

9. **Stop at the stub boundary**
   - Do not fill in algorithms, persistence, network calls, business logic, or private helper implementations.
   - Avoid building internal abstractions that are not needed to express the public API.
   - Summarize the public interface that was stubbed, the intentional placeholders, and the next implementation steps.

## Clarifying Questions

Ask questions when public contract decisions are ambiguous and cannot be answered from the plan or codebase. Useful topics include:

- Who or what will call this API?
- What inputs and outputs should the caller see?
- Which errors or failure states are part of the contract?
- Should the API be synchronous or asynchronous?
- What should be public, private, exported, or re-exported?
- Are names, data shapes, or module boundaries already established by the plan?

Do not ask questions merely to avoid reading the codebase. Inspect relevant existing patterns first.

## Final Response

When finished, briefly report:

- The data structures and public functions, methods, or interfaces that were stubbed.
- The files changed.
- The validation commands run and whether failures are expected placeholder failures or real issues.
- Any public contract decisions the user should confirm before implementation continues.
- A Mermaid diagram showing the final stubbed structure and relationships.

Prefer a `classDiagram` when the stubs define types, classes, structs, traits, interfaces, methods, fields, inheritance, implementation, composition, or other type relationships. Use another Mermaid diagram type only if it better represents the final shape, such as a flowchart for module boundaries or data flow.

Keep the diagram focused on the public contract and important relationships. Do not include speculative internals that were intentionally not stubbed.
