# Safety

Keep memory safety, FFI soundness, untrusted input, and unsafe abstractions auditable.

## `justify-unsafe-use`

Precede every `unsafe` block with a `// SAFETY:` comment that explains why the operation is sound at this call site. Cover the relevant requirements for validity, alignment, initialization, lifetime, aliasing, thread safety, and bounds. The comment is a proof obligation, not a formatting ritual. If the argument cannot be verified, shrink the unsafe scope, add a safe abstraction, or change the design.

## `document-safety-conditions`

Every `unsafe fn` and `unsafe trait` must include a `# Safety` section that states exactly what callers or implementers must uphold. Document external obligations, not implementation steps.

## `justify-unsafe-impl`

Place a `// SAFETY:` comment next to every `unsafe impl`. Explain how the implementation satisfies each relevant requirement of the unsafe trait. This is the implementation's proof, not a new obligation for callers.

## `small-audit-boundary`

Encapsulate unsafe operations and their invariants in the smallest practical module. Every piece of code that can mutate the same private state belongs to the safety argument. Do not give unrelated code write access or a way around constructors. When changing layout, field visibility, initialization, destruction, or trait implementations, recheck every unsafe operation that relies on the affected state.

## `validate-at-boundaries`

Validate untrusted data at a designated trust boundary, including user input, network data, file formats, FFI arguments, and deserialized values. Represent validated values with types or explicit invariants so internal code does not repeat inconsistent validation. Validation must preserve the external contract; do not silently clamp, truncate, or default a value when the contract requires an error.

## `ffi-contracts`

FFI code must define the ABI, layout, ownership, threading constraints, error behavior, and release responsibility. `repr(C)`, a raw pointer, or a conversion function is not a safety proof by itself. Account for null or dangling pointers, incorrect lengths, uninitialized memory, non-UTF-8 data, and callbacks that outlive their context.

## `unsafe-isolation`

Prefer a narrow safe API that proves low-level invariants once. Do not propagate `unsafe` through the call graph unless callers genuinely participate in the safety proof.

## `unsafe-review-trigger`

Re-audit related unsafe code when a change affects field types, size, alignment, or layout; construction, initialization, or `Drop`; access paths to private state; `Send`, `Sync`, or thread boundaries; pointer provenance, length, or lifetime; or synchronization and other execution-context constraints.