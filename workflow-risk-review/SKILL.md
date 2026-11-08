---
name: workflow-risk-review
description: Audit a scoped workflow or change for reachable state and invariant violations across retries, concurrency, and event ordering. Design focused regression tests from the evidence.
---

# Workflow Risk Review

Find harmful execution sequences in the requested workflow or change. Start with the state and side effects that can cause material harm. Trace adjacent code when it can change reachability or outcomes.

## Model the risky transitions

- Identify explicit states and implicit ones represented by fields, timestamps, related records, or external effects. Trace the entry points and writers that can advance them.
- Take expected invariants from requirements, established contracts, or confirmed decisions. Record observed behavior separately. Flag unclear contracts before classifying a deviation as a bug.
- Sketch only the transitions needed for the audit. For each, capture the starting state, event, guard, resulting state, side effects, and code evidence. Check where guards are enforced and which writes or effects are atomic.

## Establish reachability and impact

- Consider applicable sequences such as a duplicate or late event, a retry after partial success, or concurrent writers reading the same state. Follow the real path through guards, transactions, locks, constraints, and downstream idempotency where relevant.
- For each finding, show the violated invariant, the shortest reachable sequence with preconditions, the code locations, and the observable impact. Distinguish failures reproduced in execution, violations established by a concrete code path, and hypotheses that still need evidence. Rank confirmed findings by impact and group those that share a root cause.

## Test and report

- Prefer the smallest regression test through an existing public or integration boundary. Derive the expected result from the contract. Control the event order or interleaving directly when feasible, using existing fixtures and synchronization points.
- By default, report findings, reproduction steps, and proposed tests in the chat. When the request includes a fix or tests, add the focused regression, demonstrate the failure before the fix when practical, and report the checks actually run. Keep any durable documentation or issue creation within the requested scope.
