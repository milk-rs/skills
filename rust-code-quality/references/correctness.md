# Correctness

Make behavior correct for every reachable input, state, and error path.

## `checked-arithmetic`

Use checked or saturating arithmetic where overflow or underflow is possible. Choose `checked_*`, `saturating_*`, `overflowing_*`, or explicit `wrapping_*` according to the contract. If wraparound is intentional, make the intent and valid range visible. Do not rely on implicit release-mode wrapping.

## `numeric-conversions`

Review numeric conversions by their semantics. An infallible widening conversion is fine. When the destination must represent every input value, use `TryFrom` or prove the range first. When truncation, saturation, or bit reinterpretation is intentional, express and justify it explicitly.

## `propagate-errors`

Use `Result` and `Option` to represent recoverable outcomes. At the current abstraction level, handle, transform, retry, aggregate, degrade, or propagate them with `?` as the API contract requires. Do not hide legitimate failure behind `unwrap`, `expect`, indexing, or silent error suppression. Use `expect` when failure would violate a proven invariant, and make the message state that invariant; "this usually succeeds" is not a proof.

## `assertions-match-contract`

For external input or legitimate runtime failure, return an error or recover as the contract requires. For conditions that must protect production behavior, use a runtime check or `assert!`. For internal invariants checked only during development, use `debug_assert!` only when release behavior remains correct without the check. Never use `debug_assert!` in place of required production validation.

## `reachable-failure-analysis`

For every new `unwrap`, `expect`, index operation, or `remove(...).unwrap()`, construct a concrete input or state that could make it fail. If the failure cannot be proved unreachable, handle it explicitly. Pay particular attention to loops that mutate containers, merge neighboring ranges, remove entries, invalidate caches, or retry work; preserving logical content does not guarantee that a later container entry still exists.

## `state-invariants`

Keep state transitions centralized and visible. Review every creation, mutation, recovery, and destruction path, including errors, cancellation, re-entry, and partial initialization. Prefer types and encapsulation to comments for enforcing invariants. When an invariant must be documented, state every condition that maintains it.

## `boundary-semantics`

Distinguish empty, absent, default, invalid, and boundary values. Do not change the observable contract through silent truncation, implicit defaults, or swallowed errors.

## `raii`

Acquire and release resources through types and `Drop` when cleanup is synchronous, including lock guards, file handles, temporary files, and external handles. Use manual acquire/release pairs only when RAII cannot express the lifetime, and document why. Ensure a guard is bound for the full intended lifetime; watch for temporaries that drop before the critical section ends.

## `structured-task-lifecycle`

Give threads and asynchronous tasks an explicit lifecycle protocol. Choose and verify join, cancel or abort, detach, and shutdown behavior according to the contract. Do not assume dropping a handle waits for or stops background execution. Use an explicit async `close` or `shutdown` operation for asynchronous cleanup; `Drop` cannot await it.