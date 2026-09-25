---
name: to-tickets
description: Break a plan, specification, or conversation into implementation-ready tracer-bullet tickets with concrete code scope, design references, tests, and blocking edges.
triggers:
  - user
---

# To Tickets

Produce **implementation-ready tickets**, not backlog summaries. Each ticket must fit one fresh context and explain the outcome, integration points, implementation constraints, verification, blockers, and exclusions without relying on the originating conversation.

## Process

### 1. Gather and verify context

Read the full source spec/plan/issue, comments, linked design sections, ADRs, `CONTEXT.md`, and project rules. Trace affected code and tests to confirm paths, symbols, contracts, current behavior, prior art, migration boundaries, and deletion targets. Preserve source identifiers such as defects (`D#`), invariants (`I#`), decisions (`R#`), and open decisions (`O#`); never silently resolve an open decision.

### 2. Build the dependency graph

Prefer narrow, demoable tracer-bullet slices through every required layer. Use a foundation ticket only when it creates a tested reusable capability required by multiple slices. Each ticket must fit one fresh context and declare only direct blockers.

Use expand–migrate–contract for wide refactors: add the new form, migrate green batches, then remove the old form. The graph is complete when every requirement and regression has an owner, temporary compatibility paths have deletion owners, open decisions name the first blocked ticket, and no circular or convenience-only blockers remain.

### 3. Write implementation-ready tickets

Each ticket must include:

- **Metadata:** status, type, direct blockers, defects/invariants/decisions implemented, and exact design/ADR references.
- **What to build:** the observable outcome, its value, and this slice's boundary.
- **Scope:** concrete paths, symbols, interfaces, schemas, state changes, persistence, APIs, UI states, integrations, migration steps, and deletions.
- **Control flow:** relevant ordering, transaction boundaries, waits, retries, cancellation, timeouts, idempotency, partial failure, cleanup, and recovery.
- **Reuse:** existing modules, design-system components, test helpers, and prior-art tests to extend instead of duplicate.
- **Acceptance criteria:** falsifiable scenarios with starting state, action, and exact observable/persisted outcome, including relevant boundary, invalid, duplicate, stale, repeated-action, race, failure, recovery, cleanup, authorization, compatibility, and UI states.
- **Out of scope:** named neighboring work and its owning ticket, or an explicit exclusion.

Use exact paths and symbols when they orient implementation. Link to canonical design sections rather than duplicating them. Add a compact interface/schema/pseudocode snippet or ticket-local diagram only when it removes ambiguity. Suggested implementation details should prevent architectural guesswork without prescribing incidental line-by-line code.

### 4. Audit and confirm

Verify each ticket passes:

- **Fresh-context:** implementable without the conversation.
- **Specificity:** names seams and control flow, not only goals.
- **Sensitivity:** criteria fail for plausible broken implementations.
- **Traceability:** all requirement, design, and dependency references are valid.
- **Scope:** one coherent, independently verifiable change.
- **Lifecycle:** relevant failure, retry, cancellation, cleanup, and recovery paths are covered.
- **Migration:** old paths are removed after all callers move.
- **Verification:** each test level adds distinct value and quality gates remain intact.

Present the proposed list with title, type, blockers, delivered behavior, key seam, and requirements covered. Show an ASCII or Mermaid dependency graph for parallel branches or joins. Ask for approval unless the user requested immediate publication or already approved the exact breakdown.

### 5. Publish

Publish one issue per ticket in dependency order. For local tracking write `.scratch/<feature-slug>/issues/<NN>-<slug>.md`, blockers first, with relative links to the spec, design, and ADRs. Update the spec's rollout graph and ownership references after numbering. For remote tracking use native blocking links when available and do not modify the parent issue unless requested. The actionable frontier is every ticket whose blockers are complete.

## Ticket template

```markdown
# <NN> — <Specific outcome or capability>

**Status:** ready-for-agent
**Type:** <vertical slice | foundation | migration | verification | contract>
**Blocked by:** <NN — title>, or **None — can start immediately.**
**Fixes / Implements:** <D#, I#, R#, ADR>. Design: `<path>` §<section>.

## What to build
<Concrete end-to-end behavior or reusable capability and slice boundary.>

## Scope
- `<path>` / `<Symbol>`: <specific contract or responsibility change>.
- <Ordering, state, persistence, API/UI, failure, recovery, and compatibility obligations.>
- <Existing abstractions/tests to reuse; temporary or deleted legacy paths.>

<Compact contract snippet or diagram when useful.>

## Acceptance criteria
- [ ] <Starting state + action + exact observable and persisted/runtime result.>
- [ ] <Relevant boundary, invalid, duplicate, stale, or repeated-action case.>
- [ ] <Relevant failure, race, cancellation, cleanup, or recovery regression.>
- [ ] <Affected regressions and quality gates pass.>

## Out of scope
- <Named neighboring work and owner, or explicit exclusion.>
```

## Writing rules

Use repository vocabulary. Include concrete implementation seams and suggestions; goals alone are insufficient. Keep shared architecture in canonical docs and state only this ticket's obligations. Tie criteria to observable behavior or durable state. Keep references current and pin line references to a baseline commit when used.

