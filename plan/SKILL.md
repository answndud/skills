---
name: plan
description: Create, update, simplify, or resume implementation work from a persistent PLAN.md. Use for PLAN.md maintenance and session resumption from that file.
---

# Plan

Maintain one compact `PLAN.md` per work scope so the next session can identify the next action, its finish condition, and how to verify it. A request for an implementation outline in chat does not require a plan file.

## Location and Scope

Select the target in this order:

1. The path explicitly named by the user.
2. The existing active plan for the same work scope, including plans in `docs/` or module directories.
3. The repository's established plan location for that scope.
4. A new `PLAN.md` at the relevant module boundary, or at the repository root for repository-wide work or when no narrower boundary applies.

If multiple plans appear active for the same scope and the authoritative one is unclear, identify the candidates and ask which to use before editing. Limit plan maintenance to the selected file. Implementation follows the scope of the user's request.

## Inspect Before Writing

Read only enough context to make the active work executable:

1. applicable `AGENTS.md`
2. existing `PLAN.md`
3. files named by the user
4. obvious build, product, and nearby test files

Use `rg --files` for discovery. Do not audit the whole repository unless the user requests a broad plan from scratch.

## Preferred Shape

Keep the goal and the remaining work in execution order. For a small change, one item is enough.

```md
# PLAN.md

## Goal

<Current goal and observable finish state.>

## Active

1. <Next concrete action>
   - **완료** <Observable result>
   - **검증** <Exact command, check, or smallest discovery action>
```

Name likely files, read-only references, or material constraints when they help the next session find or execute the work. Use phases only when they clarify dependencies or grouping. Keep a short `## Backlog` only for concrete future work outside the active scope.

## Slice Rules

- Group changes and tests that together deliver one verifiable outcome. Split work when each slice can be completed and verified on its own once its prerequisites are met.
- Name the concrete change and finish condition. Use an exact verification command or observable check when known. If the check is unknown, identify the smallest action that would establish it.

## Update Rules

1. On resumption, reconcile the plan with relevant code and available verification evidence. Put the next executable work first.
2. For blocked work, record the concrete blocker and what would clear it. Keep independent executable work ahead of blocked items.
3. Remove completed slices and phases. Keep a brief note or evidence link for decisions, verification results, or checks still pending only when they affect resumption. Distinguish passed, failed, and unrun checks.
4. Preserve useful item identifiers and renumber only when it improves readability. If no executable work remains, remove `## Active` or mark it empty and retain any outstanding blockers separately.

## Language

Use Korean by default. Match repository terminology for identifiers and slice titles when that is clearer.
