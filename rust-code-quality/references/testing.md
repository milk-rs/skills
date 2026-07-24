# Testing

Tests should prove behavior, boundaries, and regression risks, not merely increase line coverage.

## `test-observable-behavior`

Prefer testing behavior through public APIs, user-visible output, or an external contract. Do not widen visibility merely to test private implementation details. Name tests after the behavior, scenario, or specification concept they verify.

## `regression-test-for-bug-fix`

Every bug fix should include a regression test that fails before the fix, unless the failure cannot be reproduced reliably. When no stable regression test is possible, record why and provide an alternative verification method. The test should exercise the triggering input, state transition, interleaving, or resource lifetime, not only the repaired happy path.

## `boundary-and-error-cases`

Consider empty, minimum, maximum, overflow, missing-resource, repeated-call, mid-operation failure, cancellation, and concurrent-interleaving cases. For external input, include invalid format, length, permission, and lifetime cases when relevant. Add contract-relevant boundaries; do not manufacture fragile tests to increase the count.

## `assertions-not-printing`

Use assertion macros or test-framework checks instead of printing values for manual inspection. Failure messages should contain enough context to diagnose the failure without interaction.

## `deterministic-isolated-tests`

Keep tests deterministic, independent, and repeatable. Clean up files, descriptors, threads, child processes, temporary directories, registry entries, and background tasks. Do not depend on state left by another test. For concurrency tests, prefer controlled synchronization points, virtual time, or model checking over arbitrary sleeps and retry counts.

## `test-the-contract`

Tests should protect the public contract, critical invariants, and failure behavior. Do not test default values, log text, or a container type unless it is itself a stable contract.

## `verification-scope`

Run checks that match the change: start with a fast check for the affected crate or module, then run the broader suite required by the repository. Report the commands actually run and their results; do not overstate the verification scope.