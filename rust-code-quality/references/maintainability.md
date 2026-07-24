# Maintainability

Write code to minimize the time another person needs to understand, modify, and verify it.

## Design

### `single-responsibility`

Give each module, type, and function one clear reason to change. Do not mix abstraction levels in one function: an entry point should express the flow, while parsing, conversion, and low-level details belong in well-named helpers. Split a file when it contains independent concepts, but only when the split reduces cognitive load.

### `information-hiding`

Hide implementation details behind a well-defined interface. Expose only what consumers need; keep bookkeeping state, construction constraints, and internal representation private.

### `coupling-cohesion`

Keep connections between modules small, visible, and stable. Within a module, every part should contribute to one well-defined purpose.

### `consistency`

Do similar things the same way throughout the codebase. Follow existing naming, error, logging, module, and testing patterns instead of introducing a competing convention without a compelling reason.

### `least-surprise`

Names, signatures, and behavior should agree. Use familiar Rust terms for familiar operations, and do not give a familiar name to behavior that violates its usual contract.

### `rust-native`

Write idiomatic Rust rather than translating manual conventions from another language. Prefer `?`, RAII, trait bounds, ownership, and type states when they can enforce rules that would otherwise depend on caller discipline.

### `avoid-premature-extension`

Do not add traits, callbacks, configuration, or abstraction layers for hypothetical needs. Add an extension point when a concrete consumer requires it.

## Naming

### `descriptive-names`

Choose names that convey meaning at the point of use. Avoid meaningless single letters, ambiguous abbreviations, and compressed names that force the reader to recover context from surrounding code.

### `accurate-names`

Names must describe behavior, results, and side effects accurately. Do not make I/O, traversal, allocation, or mutation look like a simple field access.

### `encode-units`

When the type does not carry the unit, put it in the name, such as `timeout_ns`, `size_pages`, or `offset_bytes`. If the unit is an important domain invariant, prefer a newtype.

### `no-magic-number`

Give semantic names to literals that encode protocol values, masks, limits, offsets, or domain rules. Use a constant, enum, type, or helper that expresses the invariant. Do not name ordinary `0`, `1`, or `2` values merely for formality.

### `bool-names`

Boolean values and predicates should read as assertions of fact. Prefer prefixes such as `is_`, `has_`, `can_`, `should_`, and `needs_`. Avoid negated names; prefer `is_empty` to `is_not_empty`.

## Layout and comments

### `top-down-reading`

Organize a file from high-level entry points and core flow to implementation details. Place public methods before private helpers, and callers before callees where practical.

### `logical-paragraphs`

Group related statements into blank-line-separated logical paragraphs. Each paragraph should represent one sub-step. For a long function, add a one-line intent comment only when the paragraph is not self-explanatory.

### `explain-why`

Comments should explain intent, rationale, dependencies, and risks, not restate what the code does. If a comment must explain what the code does, first try to make the code straightforward.

### `design-decisions`

Document non-obvious choices such as data structures, locking strategies, compatibility deviations, performance tradeoffs, and safety assumptions. Include rationale and relevant alternatives when they affect future changes.

### `cite-sources`

When behavior comes from an external specification, ABI, protocol, or non-trivial algorithm, cite the authoritative specification, manual, paper, or issue that supports the implementation.

### `narrow-visibility`

Start private. Widen to `pub(super)`, `pub(crate)`, or `pub` only when an actual consumer requires it. Wider visibility increases both the compatibility promise and the audit surface.