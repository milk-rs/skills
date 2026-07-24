# Concurrency

Make behavior correct across threads, asynchronous tasks, and shared state.

## `lock-ordering`

When code can acquire multiple locks, establish one consistent and verifiable lock order. Document it near the relevant module or function; do not rely on callers to acquire locks in the usual order. After adding a lock or changing a call path, check every path for a possible reverse acquisition order.

## `atomic-critical-sections`

Keep a check-then-act operation within one critical section. Do not assume that state remains unchanged between two lock acquisitions, atomic loads, or `await` points. If one critical section is impossible, re-read and validate the state or use an API that expresses an atomic transition.

## `careful-atomics`

When multiple fields must remain consistent, prefer one lock or one state machine. Use a multi-atomic lock-free design only when it has a concrete benefit and its state protocol can be proved. Choose memory ordering from the required happens-before relationships; do not choose `Relaxed` merely because it is faster or common.

## `guard-lifetime`

Keep a lock guard and its borrows alive for the full critical section, but do not extend them across `await`, callbacks, or unbounded work without a reason. Whether I/O or long computation belongs inside a critical section depends on the atomicity contract; when it does, make the reason and synchronization primitive explicit. Check for temporary guards that drop immediately and explicit `drop` calls that release state before a later operation. Holding a synchronous mutex guard across `await` can block an executor or deadlock; restructure the critical section or use an async-compatible primitive when needed.

## `send-sync-and-ownership`

Before sending a value across threads or tasks, confirm that its `Send`, `Sync`, shared-ownership, and destruction semantics match the contract. Do not use `Arc<Mutex<_>>` to hide an unclear ownership model.

## `async-cancellation`

An asynchronous operation may be cancelled when its future is dropped while pending. Check whether partially completed state, locks, registrations, timers, resources, and external side effects can be safely recovered or cleaned up. Do not assume that an async function runs from start to finish; make cancellation safety explicit where the operation requires it.