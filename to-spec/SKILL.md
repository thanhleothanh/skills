---
name: to-spec
description: Turn the conversation and repository evidence into an implementation-ready specification with concrete design, code references, diagrams, tests, and rollout guidance.
triggers:
  - user
---

# To Spec

Produce an **implementation-ready specification**, not a feature brief. A fresh agent must understand the current system, the gap, the target design, where it integrates, and how to verify it without reconstructing the design from the conversation.

Do not interview the user. Record unresolved choices as open decisions with a recommendation, rationale, and the work they block.

## Process

### 1. Establish the baseline

Trace every affected behavior from entry point to observable output. Read `CONTEXT.md`, relevant ADRs, canonical docs, project rules, implementation, and tests. Identify current paths, symbols, integration seams, prior art, and the commit or working-tree baseline for code references. Label assumptions; do not invent repository facts.

### 2. Diagnose and define behavior

- State the user-visible problem and operational impact.
- Create a numbered defect/gap inventory (`D1`, `D2`, …) when useful. For each item give the scenario, expected versus actual behavior, root cause, and code evidence.
- Define meaningful user stories and numbered invariants (`I1`, `I2`, …) covering ownership, ordering, idempotency, concurrency, failure, recovery, cleanup, security, compatibility, and observability as applicable.
- Map every defect to an invariant, decision, or explicit exclusion.

### 3. Design the implementation

Give concrete, repository-grounded guidance:

- target architecture, ownership boundaries, and existing abstractions to reuse;
- modules and symbols to add, change, migrate, or remove;
- interfaces, schemas, state machines, persistence, APIs, UI states, and external contracts;
- runtime ordering, transactions, awaits, retries, cancellation, timeouts, late results, cleanup, and recovery;
- migration and compatibility behavior while old and new paths coexist;
- security, authorization, secret handling, logging, and operational implications.

Use compact type/schema/pseudocode snippets when they express a contract better than prose. Use Mermaid or ASCII diagrams for non-obvious topology, lifecycle, sequence, or rollout dependencies. Reference exact canonical design and ADR sections. Create/update a deeper technical design when the contract is too large for the spec; create an ADR only for a durable architectural decision.

### 4. Record decisions, tests, and rollout

- Number resolved decisions (`R1`, `R2`, …) with rationale and consequences.
- Number open decisions (`O1`, `O2`, …) with a recommended default and blocked ticket/phase.
- Choose the highest stable behavioral test seam. Define pure units, integrations, browser/real-service tests only where distinct, deterministic fakes/gates/clocks, required regressions, and a scenario matrix for relevant normal, boundary, invalid, duplicate, failure, race, cancellation, recovery, and cleanup paths.
- Plan delivery in green increments: foundations, incremental caller migrations, and explicit legacy deletion. Use expand–migrate–contract for wide refactors and include a dependency graph for non-linear work.

### 5. Publish

Publish to the configured tracker with `ready-for-agent`. For a local tracker write `.scratch/<feature-slug>/spec.md`; use relative links to docs and ADRs. Create tickets only when requested.

## Spec template

```markdown
---
title: "<specific target outcome>"
created: <YYYY-MM-DD>
status: ready-for-agent
baseline: <commit or working tree>
design: <canonical design path, if any>
adrs: [<applicable ADRs>]
---

# <Feature or redesign>
<Orientation, superseded material, design links, and reference baseline.>

## 1. Problem statement
## 2. Current-state defect or gap inventory
| ID | Scenario and actual behavior | Root cause and code evidence | Target |
| --- | --- | --- | --- |
| D1 | ... | `path/file.ts:<lines>` / `Symbol` | I1, R1 |

## 3. Goals, user stories, and invariants
## 4. Solution summary
<Architecture summary and useful diagram.>

## 5. Implementation design
### Modules and ownership
### Interfaces and contracts
### Data, persistence, and APIs
### Runtime sequences and state transitions
### Failure, recovery, and cleanup
### Compatibility, migration, security, and observability

## 6. Decisions
### Resolved
### Open
## 7. Testing decisions
## 8. Rollout order
<Phases and dependency graph.>
## 9. Out of scope
## 10. References
```

## Quality bar

The spec is complete only when a fresh agent knows where to start, how the design fits the repository, which contracts and edge cases govern it, and how success is proven. Ground important claims in code, docs, ADRs, or labeled assumptions; cross-reference defects, invariants, decisions, tests, and rollout; use diagrams only where they clarify real complexity.

