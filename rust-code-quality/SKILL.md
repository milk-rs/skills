---
name: rust-code-quality
description: Improve Rust code quality during implementation, refactoring, self-review, and documentation work. Use when writing or reviewing Rust code involving API design, type invariants, error handling, unsafe code, concurrency, resource lifetimes, performance, tests, rustdoc, or crate documentation.
---

# Rust Code Quality

## Goal

Write Rust code that is easy to understand, maintain, and verify. Fix real problems without adding abstractions, copies, or complexity merely to satisfy a rule.

Use this skill when writing or modifying Rust code; refactoring modules, types, or APIs; reviewing a Rust diff or file set; working with `unsafe`, concurrency, resource lifetimes, performance, or error paths; designing regression tests; or writing rustdoc, crate documentation, or Rust-focused Markdown.

Do not treat conventions from another project or specialized domain as universal Rust rules. The current repository's established conventions take precedence.

## Workflow

### 1. Establish context

- Read repository instructions, README, contribution guides, and relevant module documentation.
- Find similar code and reuse established naming, error, ownership, and testing patterns.
- Before changing a public symbol, inspect its definition, references, implementations, and re-exports.
- State the behavior, boundaries, error paths, and invariants affected by the change.

### 2. Load guidance by risk

Always read `references/maintainability.md`. Read the other references when applicable:

- Types, traits, lifetimes, or public APIs: `references/api-and-types.md`
- Error handling, arithmetic, state machines, or boundary logic: `references/correctness.md`
- `unsafe`, pointers, FFI, layout, or untrusted input: `references/safety.md`
- Locks, atomics, channels, threads, or cancellation: `references/concurrency.md`
- Allocations, clones, hot paths, or optimization: `references/performance.md`
- New behavior, bug fixes, or test changes: `references/testing.md`
- Markdown, rustdoc, README files, or published crate documentation: `references/documentation.md`

Use these guidelines to surface risks and guide judgment. They do not replace reasoning about the actual code and its contract.

### 3. Design and implement

- Make the smallest change that expresses the intended behavior clearly.
- Use types, ownership, and API shape to enforce invariants.
- Keep the expected path flat; handle errors and edge cases early.
- Justify each `unsafe` use, panic path, lock boundary, and manual resource release.
- Review clones, allocations, buffer copies, and serialization when they have meaningful cost or ownership impact.
- Do not add extension points for hypothetical future requirements.
- Prefer clarity over brevity when shorter code takes longer to understand.

### 4. Verify

Use the repository's own commands and configuration. Applicable checks commonly include formatting, `cargo check` for affected members and features, repository-configured Clippy, affected tests, and a smoke test for changed behavior.

If a check cannot run, state the exact reason. Never report an unexecuted check as verified.

### 5. Self-review

Before finishing, ask:

- Did the change alter undeclared behavior or a public API?
- Does any reachable path still panic, swallow an error, overflow, or truncate unexpectedly?
- Did the change weaken an ownership, lifetime, concurrency, or resource-release invariant?
- Did it add an unnecessary clone, allocation, lock contention point, or abstraction?
- Do the tests protect observable behavior and meaningful failure paths?
- Does the result follow this repository's conventions rather than another project's conventions?

## Conflict priority

When guidelines conflict, use this order: Rust's language and memory-safety guarantees; the current project's explicit conventions and public contracts; runtime correctness, error handling, and concurrency safety; maintainability, readability, and API stability; evidence-supported performance requirements; brevity and local style preferences.

No guideline is unconditional. When the actual contract justifies an exception, keep the exception and record the reason when it is not obvious.

## Output requirements

When asked to modify code, implement and verify the change rather than returning advice alone. When reviewing code, each finding must include a precise location, a reproducible failure scenario or violated invariant, severity, the smallest viable fix, and the relevant guideline ID when one applies.

Report only findings supported by evidence. Mark unresolved suspicions as requiring further verification.