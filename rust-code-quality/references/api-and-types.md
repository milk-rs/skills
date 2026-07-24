# Types and APIs

Use types, ownership, and interfaces to express the domain contract.

## `rust-type-invariants`

Use the type system to make illegal states unrepresentable. Use newtypes, enums, private fields, constructors, generic parameters, and type states to encode ranges, units, permissions, initialization, and resource ownership. Do not represent a constrained domain value with a bare integer, string, or boolean when the primitive admits invalid states. Keep the primitive when the constraint is local and obvious and a new abstraction would add more noise than safety.

## `enum-over-dyn`

For a known, closed set of variants, prefer an enum over `Box<dyn Trait>` when exhaustive matching expresses the design better. An enum also commonly avoids dynamic dispatch and a separate allocation. Trait objects remain appropriate for open extension sets, plugin boundaries, runtime polymorphism, and interfaces that require object safety.

## `ownership-matches-lifetime`

Make parameters and return types reflect the ownership the operation actually needs. Borrow when ownership is unnecessary; do not clone or introduce `Arc` merely to avoid designing a clear lifetime. Use shared ownership when work crosses threads or tasks, enters a cache, or otherwise outlives the caller. Check the lifetimes of guards, references, iterators, and temporaries so resources are not released too early or kept alive accidentally.

## `getter-encapsulation`

Prefer a getter over a public field when the field is part of an abstraction. A private field preserves naming freedom and leaves room for invariants, caching, and validation. A public field is reasonable when it is intentionally part of a stable data contract.

## `no-bool-args`

Avoid a boolean parameter that selects between two distinct behaviors. Split the function or use a typed enum that gives the choice a name. A boolean can remain in a local helper when it represents one unambiguous binary property.

## `public-api-minimal`

Expose only what actual consumers need. Before adding `pub`, a trait implementation, a constructor, or mutable access, check whether it bypasses an invariant, expands a compatibility promise, or increases documentation burden.

## `error-types-carry-context`

Error types should preserve the context callers need to choose a response. Do not replace distinguishable failures with an undifferentiated string, boolean, or overly broad error. Public errors should describe the observable contract, not irrelevant implementation details.