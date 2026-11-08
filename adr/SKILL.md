---
name: adr
description: Create, update, or reconcile architecture decision records in ADR.md, individual ADR files, or an established technical decision log.
---

# ADR

Maintain one compact architecture decision record file:

```text
ADR.md = significant technical decisions and their evidence
```

Write it for future implementation. It should let an agent understand which decisions are already made, why they matter, what tradeoffs exist, and what evidence supports them.

## Location and Scope

Determine the target scope in this order:

1. path explicitly named by the user
2. existing active ADR or decision-log convention
3. independent product, service, package, or module boundary
4. nearest applicable `AGENTS.md` or `CLAUDE.md` when it represents that boundary
5. repository root

Default target is the selected scope's `ADR.md`. If `docs/ADR.md` or `docs/adr/**` is the active repository convention, keep it as the target. If it is clearly legacy or superseded, merge or migrate useful content into the selected target unless the user asks to preserve it. If both paths contain materially different active decisions, do not overwrite either file; ask which document is authoritative when interaction is available, otherwise report a proposed merge without writing it.

Limit edits to the selected ADR or log. When the requested change supersedes a decision, also update its record if the repository keeps it in a separate file. Do not create `docs/ADR.md` by default.

Do not create `AGENTS.md`. Add an `AGENTS.md` pointer only when the user asks for it.

## Inspect Before Writing

Read enough context to record real decisions:

1. applicable `AGENTS.md` or `CLAUDE.md`
2. existing `ADR.md`, `docs/adr/**`, or equivalent decision logs
3. files named by the user
4. `README.md`, manifests, CI, scripts, source entrypoints, schemas, tests, and public interfaces that reveal durable choices

Use `rg --files` when available; otherwise use the agent's equivalent file-discovery mechanism. Do not deep-audit the whole repository unless the user asks for a full decision reconstruction.

## What Counts as an ADR

Record decisions that materially constrain future implementation, such as:

- framework, runtime, language, package manager, or build system
- storage, schema, migration, or data ownership model
- API style, CLI surface, event model, or integration boundary
- auth, permissions, trust boundaries, or security posture
- deployment, operations, configuration, or environment model
- state management, testing architecture, or compatibility strategy

Do not record routine code organization, minor refactors, task progress, changelog entries, or wishes for future work.

## Preferred Shape

```md
# ADR.md

## ADR-0001 - <decision title>

- 상태: accepted | proposed | superseded | deprecated
- 날짜: YYYY-MM-DD | Date unknown
- 근거 유형: explicit | inferred

### Context

<Problem, constraint, or force that required the decision.>

### Decision

<Chosen approach.>

### Alternatives

<Include only when evidenced, user-provided, or clearly labeled as a material inference. Otherwise omit this section.>

### Consequences

- <Positive or negative implication>

### Evidence

- `<path>`: <what this proves>

### Open Questions

- <Only if unresolved>
```

Keep numbering stable. Add new entries instead of renumbering existing ADRs unless the file is clearly new and unreferenced.

## Questions and Conflicts

Ask only questions whose answers would materially change the decision status, chosen option, consequences, or whether an item deserves an ADR. If missing information is not blocking, proceed with a reviewable entry and mark it as `가정`, `추론`, or `오픈 질문`.

Use explicit decision records or user direction to establish what was decided. Use config, code, tests, and build behavior to establish what was implemented. If implementation differs from an active decision, report the mismatch and preserve the decision until an authoritative change is confirmed.

## Evidence Rules

Record only decisions with evidence or explicit user direction.

- Use `근거 유형: explicit` when an authoritative record or user direction states the decision. Set `accepted` only when the evidence establishes that the choice was adopted as a decision.
- Use `근거 유형: inferred` for a choice reconstructed from implementation evidence. Record it as an observation or qualified inference. The implementation alone does not establish approval, rationale, or decision date.
- Label uncertainty directly; do not create fake history.
- Use `Date unknown` when the decision date is not known.
- Keep enough context to make each decision understandable without previous chat history.

Do not invent alternatives, motivations, dates, owners, or prior debates. If alternatives are not evidenced, write plausible alternatives as `추론` or omit them.

## Update Rules

Treat `ADR.md` as a durable decision log:

1. Preserve existing ADR IDs and recorded rationale. Change status only when the decision lifecycle change is supported by evidence.
2. Add or update entries only for significant decisions.
3. When a replacement decision is confirmed, add or identify the new entry, mark the old entry `superseded`, and cross-reference both entries.
4. Link decisions to concrete repository evidence.
5. Keep current decisions separate from proposals.

If an important technical choice belongs in the system description instead of decision history, put it in `TRD.md` rather than forcing an ADR.

## Consistency Check

Before finalizing:

- statuses are valid
- inferred decisions are labeled
- entries cite concrete evidence
- no fake dates or invented rationale were added
- material mismatches between active decisions and current implementation are identified

## Verification

After editing:

1. Confirm the target path.
2. Re-read all changed ADR entries.
3. Inspect the final diff for unintended deletion, renumbering, or unrelated changes.
4. Search for accidental placeholders such as `TBD`, `TODO`, `<...>`, or copied template text.
5. Check each changed entry has status, date, evidence type, decision, consequences, and evidence.
6. Confirm inferred alternatives or rationale are labeled and no fake dates or history were added.

Run repository tests only when the user also asked for implementation validation.

## Final Response

Report concisely:

- ADR path created or updated
- decisions added or updated
- evidence inspected
- verification performed

Use Korean by default unless the repository or user clearly prefers another language.
