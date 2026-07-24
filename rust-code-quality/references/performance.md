# Performance

Consider real time and resource costs without adding complexity for an unmeasured problem.

## `measure-before-optimizing`

Support a claimed performance improvement with reproducible measurements, profiling, or complexity analysis. Confirm that the change is on the affected path, and record the baseline, workload, and result. Do not introduce obscure caching, unsafe code, concurrency, or data structures for a merely assumed performance problem.

## `minimize-copies`

Borrow when ownership is unnecessary; do not clone an `Arc` when a reference is sufficient; do not collect an iterator when materialization is unnecessary. Review clones, heap allocations, buffer copies, and serialization when they have meaningful cost or ownership impact, and explain non-obvious choices. Ordinary `Copy` values and small-value passing do not require a comment. Do not remove a small copy at the cost of less clear lifetimes or APIs.

## `hot-path-complexity`

Frequently executed paths with growing input should not introduce an unexamined O(n) scan. Use actual scale, frequency, and profiling data to decide whether a lower-complexity structure is needed. Theoretical O(n) complexity is not a defect by itself; show that it creates observable cost or an extension risk on the current path.

## `allocation-boundaries`

Check for implicit allocations in loops, error paths, logging paths, and external boundaries. When a path has a zero-allocation requirement or budget, express that constraint through its API, buffer reuse, or type design.

## `readability-over-micro-optimization`

A small performance gain does not by itself justify extra abstraction, copy control, or unsafe code. Prefer Rust code that the compiler can optimize while remaining direct and readable.

## `resource-costs`

Consider memory, lock contention, file descriptors, threads, tasks, network round trips, and cache effects in addition to CPU time. Performance analysis should cover the actual bottleneck, not only the local instruction count.