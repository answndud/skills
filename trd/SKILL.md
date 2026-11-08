---
name: trd
description: Create, update, or reconcile TRD.md or an equivalent technical design document that records system boundaries, contracts, constraints, and how to verify them.
---

# TRD

Maintain one compact technical requirements and design file:

```text
TRD.md = current system design, contracts, constraints, risks, and verification
```

Write it for future implementation. It should let an agent understand how the system is built, where changes belong, which contracts must hold, and how to verify technical correctness.

## Location and Scope

Determine the target scope in this order:

1. path explicitly named by the user
2. existing active TRD or technical-document convention
3. independent product, service, package, or module boundary
4. nearest applicable `AGENTS.md` or `CLAUDE.md` when it represents that boundary
5. repository root

Default target is the selected scope's `TRD.md`. If `docs/TRD.md` is the active repository convention, keep it as the target. If it is clearly legacy or superseded, merge or migrate useful content into the selected target unless the user asks to preserve it. If both paths contain materially different active constraints, do not overwrite either file; ask which document is authoritative when interaction is available, otherwise report a proposed merge without writing it.

Edit only the selected target document unless the user explicitly requests other files. Do not create `docs/TRD.md` by default.

Do not create `AGENTS.md`. Add an `AGENTS.md` pointer only when the user asks for it.

## Inspect Before Writing

Read enough repository evidence to avoid architecture fiction:

1. applicable `AGENTS.md` or `CLAUDE.md`
2. existing `TRD.md` or equivalent design docs
3. files named by the user
4. `README.md`, package/build manifests, CI, scripts, source entrypoints, schemas, tests, and public interfaces

Use `rg --files` when available; otherwise use the agent's equivalent file-discovery mechanism. Inspect representative files, not the whole repository, unless the user asks for a broad technical reconstruction.

## Required Content

Keep only implementation-relevant technical state:

- system summary and runtime boundaries
- key modules and ownership of responsibilities
- data, API, CLI, event, storage, or external service contracts
- important flows and failure modes
- configuration, environment, and operational constraints
- security, trust boundaries, and data handling when relevant
- durable verification methods for material technical contracts, with exact existing commands or test references when known
- technical risks, assumptions, and open questions
- enough context to make the document understandable without previous chat history

Exclude product requirements, business goals, task lists, changelogs, command logs, code dumps, and decision-history prose. Put product scope in `PRD.md`; put significant decisions in `ADR.md`; put executable work in `PLAN.md`.

## Preferred Shape

```md
# TRD.md

## System Summary

<Current technical shape and finish state.>

## Architecture

- <Module/component>: <responsibility and key files>

## Contracts

- <Interface/schema/API/CLI/event>: <inputs, outputs, invariants>

## Flows

1. <Important runtime or data flow>

## Constraints and Risks

- <Constraint, risk, or trust boundary>

## Verification

- <Material contract and the test, command, or observable check that verifies it>

## Assumptions and Open Questions

- <Assumption or unresolved technical decision>
```

Use a smaller shape when the system is small. Add diagrams only when they make relationships clearer than text.

## Questions and Conflicts

Mark an open decision as blocking only if the answer materially changes architecture boundaries, external contracts, data handling, safety constraints, or the ability to verify a required outcome. Draft the settled sections and identify what the decision blocks. Label lower-impact unknowns as `가정`, `제안`, or `오픈 질문` and keep the draft moving.

For current-state technical claims, prefer observable code, config, tests, and build behavior over stale prose. For intended future design, prefer explicit current user direction. Do not silently resolve material conflicts; record them as open questions or stop and ask when writing would overwrite conflicting active constraints.

## Evidence Rules

Ground technical claims in repository evidence.

- Cite concrete paths when they materially help future agents.
- Mark inferred claims as `추론`.
- Mark unavailable information as `오픈 질문`.
- Distinguish the implementation observed in the repository from the target design explicitly confirmed by the user. Label unconfirmed target choices as `제안` or `오픈 질문`.

Do not invent architecture, contracts, deployment topology, database semantics, security guarantees, or migration history.

## Update Rules

Treat `TRD.md` as the current technical contract:

1. Preserve accurate existing design notes.
2. Replace stale claims only with repository evidence or user direction.
3. Convert vague architecture prose into concrete modules, contracts, flows, and verification.
4. Keep implementation constraints visible near the affected area.
5. Tie each documented check to the contract it verifies. Report results from the current run in the work summary. If an existing `PLAN.md` tracks the work, keep only results or pending checks that affect resumption there.

Do not rewrite wholesale when a focused merge is safer.

## Verification

After editing:

1. Confirm the target path.
2. Re-read the complete target TRD.
3. Inspect the final diff for unintended deletion or unrelated changes.
4. Confirm current implementation, intended design, assumptions, and open questions are not mixed.
5. Check that referenced contracts, paths, and commands exist or are clearly marked as proposed or unverified.
6. Search for accidental placeholders such as `TBD`, `TODO`, `<...>`, or copied template text.
7. Check that technical claims are evidenced, user-provided, inferred, or marked as open questions.

For document-only changes, start by inspecting the referenced contracts and checks. Run a focused test if a material claim about current behavior needs execution evidence, and follow any broader verification the user requests.

## Final Response

Report concisely:

- TRD path created or updated
- context inspected
- key constraints or open questions
- verification performed

Use Korean by default unless the repository or user clearly prefers another language.
