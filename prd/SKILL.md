---
name: prd
description: Create, update, or reconcile PRD.md or an equivalent product requirements document that records intended behavior, scope, and acceptance criteria.
---

# PRD

Maintain one compact product requirements file:

```text
PRD.md = product intent, scope, requirements, and acceptance criteria
```

Write it for future implementation. It should let an agent understand what product outcome to build, who it serves, what is in or out of scope, and how completion will be judged.

## Location and Scope

Determine the target scope in this order:

1. path explicitly named by the user
2. existing active PRD or product-document convention
3. independent product, service, package, or module boundary
4. nearest applicable `AGENTS.md` or `CLAUDE.md` when it represents that boundary
5. repository root

Default target is the selected scope's `PRD.md`. If `docs/PRD.md` is the active repository convention, keep it as the target. If it is clearly legacy or superseded, merge or migrate useful content into the selected target unless the user asks to preserve it. If both paths contain materially different active requirements, do not overwrite either file; ask which document is authoritative when interaction is available, otherwise report a proposed merge without writing it.

Edit only the selected target document unless the user explicitly requests other files. Do not create `docs/PRD.md` by default.

Do not create `AGENTS.md`. Add an `AGENTS.md` pointer only when the user asks for it.

## Inspect Before Writing

Read only enough context to avoid a generic template:

1. applicable `AGENTS.md` or `CLAUDE.md`
2. existing `PRD.md` or equivalent product docs
3. files named by the user
4. `README.md`, app entrypoints, visible routes, public commands, schemas, or tests that reveal product behavior

Use `rg --files` when available; otherwise use the agent's equivalent file-discovery mechanism. Do not deep-audit the whole repository unless the user asks for a full product reconstruction.

## Required Content

Keep only product-level information:

- product summary and product or feature goal
- target users or actors
- user problems and primary scenarios
- in-scope and out-of-scope behavior
- functional requirements
- non-functional requirements when product-relevant
- acceptance criteria or observable finish conditions
- success metrics when explicitly provided
- missing metrics as open questions when needed to judge the product goal
- priority such as Must/Should/Could or MVP/Later only when it changes active scope, delivery order, or completion criteria
- assumptions and open questions
- enough context to make the document understandable without previous chat history

Exclude implementation architecture, task plans, changelogs, command logs, code dumps, detailed API contracts, and decision history. Put technical design in `TRD.md`; put significant decisions in `ADR.md`; put executable work in `PLAN.md`.

## Preferred Shape

```md
# PRD.md

## Summary

<What the product or feature is and what finished means.>

## Users and Problems

- <Actor>: <problem or need>

## Scope

### In

- <Included behavior>

### Out

- <Excluded behavior>

## Requirements

1. <Observable product requirement>

## Acceptance Criteria

- <User-visible or externally observable completion condition>

## Assumptions and Open Questions

- <Assumption or unresolved product decision>
```

Use a smaller shape for tiny PRDs. Add sections only when they reduce ambiguity.

For multi-requirement PRDs, use stable IDs such as `FR-001` and `NFR-001`, and map acceptance criteria back to the requirement, for example `AC-FR-001-01`. For tiny PRDs, plain bullets are acceptable if the mapping is obvious.

## Questions and Conflicts

Mark an open decision as blocking only if the answer materially changes active scope, target users, required behavior, or acceptance criteria. Draft the settled sections and identify what the decision blocks. Label lower-impact unknowns as `가정`, `제안`, or `오픈 질문` and keep the draft moving.

For current-state claims, prefer observable repository behavior over stale prose. For intended future behavior, prefer explicit current user direction. Do not silently resolve material conflicts; record them as open questions or stop and ask when writing would overwrite conflicting active requirements.

## Evidence Rules

Ground claims in repository evidence or explicit user input.

- If repository evidence directly supports current behavior, write it as confirmed current behavior.
- Record the user's confirmed requirements and constraints. Keep user-reported current behavior separate and attribute it until verified.
- If you infer it from code, dependencies, routes, tests, or names, label it as `추론`.
- If it affects scope but is not known, label it as `오픈 질문`.

Repository evidence may prove current behavior, but not necessarily intended requirements. Distinguish `현재 동작` from `요구 동작` when they differ. For material inferences, include the evidence path when useful.

Do not invent target users, business goals, success metrics, or future roadmap. If the user asks for a proposed PRD, clearly separate `제안` from `현재 확인된 내용`.

## Update Rules

Treat `PRD.md` as the current product contract:

1. Preserve confirmed requirements until the user or an authoritative product decision changes them. If current code or tests fall short, record the implementation gap without changing the requirement or acceptance criteria.
2. Correct stale descriptions of current behavior when evidence supports the correction. Consolidate duplicate wording while preserving its requirements and constraints.
3. Convert vague goals into observable requirements.
4. Keep future ideas short and separate from active scope.
5. Ensure acceptance criteria map back to requirements.

Do not rewrite wholesale when a focused merge is safer.

## Verification

After editing:

1. Confirm the target path.
2. Re-read the complete target PRD.
3. Inspect the final diff for unintended deletion or unrelated changes.
4. Confirm active requirements are observable and have acceptance criteria.
5. Confirm scope-in and scope-out do not contradict each other.
6. Confirm current behavior, proposed behavior, assumptions, and open questions are not mixed.
7. Search for accidental placeholders such as `TBD`, `TODO`, `<...>`, or copied template text.
8. Check that product claims are either evidenced, user-provided, inferred, or marked as open questions.
9. Confirm implementation details have not leaked into the PRD.

Run repository tests only when the user also asked for implementation validation.

## Final Response

Report concisely:

- PRD path created or updated
- context inspected
- major assumptions or open questions
- verification performed

Use Korean by default unless the repository or user clearly prefers another language.
