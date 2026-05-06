# CONTEXT.md Format

Contexts live in `.docs/contexts/` and use sequential numbering: `CONTEXT-MAP.md`, `0001-CONTEXT-slug.md`, `0002-CONTEXT-slug.md`, etc.

Create the `.docs/contexts/` directory lazily — only when the first context is needed.

## Structure

```md
# {Context Name}

{One or two sentence description of what this context is and why it exists.}

## Language

**Order**:
{A concise description of the term}
_Avoid_: Purchase, transaction

**Invoice**:
A request for payment sent to a customer after delivery.
_Avoid_: Bill, payment request

**Customer**:
A person or organization that places orders.
_Avoid_: Client, buyer, account
```

## Rules

- **Be opinionated.** When multiple words exist for the same concept, pick the best one and list the others as aliases to avoid.
- **Flag conflicts explicitly.** If a term is used ambiguously, call it out in "Flagged ambiguities" with a clear resolution.
- **Keep definitions tight.** One sentence max. Define what it IS, not what it does.
- **Show relationships.** Use bold term names and express cardinality where obvious.
- **Only include terms specific to this project's context.** General programming concepts (timeouts, error types, utility patterns) don't belong even if the project uses them extensively. Before adding a term, ask: is this a concept unique to this context, or a general programming concept? Only the former belongs.
- **Group terms under subheadings** when natural clusters emerge. If all terms belong to a single cohesive area, a flat list is fine.
- **Write an example dialogue.** A conversation between a dev and a domain expert that demonstrates how the terms interact naturally and clarifies boundaries between related concepts.

## Context and Context Map

**Context:** One `0001-CONTEXT-slug.md` per context

**Context Map:** A `CONTEXT-MAP.md` at the `.docs/contexts` root lists the relationships of the contexts, where they live, and how they relate to each other:

```md
# Context Map

## Contexts

- [Order](./0001-CONTEXT-Order.md) — receives and tracks customer orders
  ...
- [Bill](./0004-CONTEXT-Bill.md) — generates invoices and processes payments
  ...
- [Fulfillment](./0004-CONTEXT-Fulfillment.md) — manages warehouse picking and shipping

## Relationships

- An **Order** produces one or more **Invoices**
- An **Invoice** belongs to exactly one **Customer**

## Interactions

- **Order → Fulfillment**: Order emits `OrderPlaced` events; Fulfillment consumes them to start picking
- **Fulfillment → Bill**: Fulfillment emits `ShipmentDispatched` events; Bill consumes them to generate invoices
- **Order ↔ Bill**: Shared types for `CustomerId` and `Money`

## Example dialogue

> **Dev:** "When a **Customer** places an **Order**, do we create the **Invoice** immediately?"
> **Domain expert:** "No — an **Invoice** is only generated once a **Fulfillment** is confirmed."

## Flagged ambiguities

- "account" was used to mean both **Customer** and **User** — resolved: these are distinct concepts.
```

The skill infers which structure applies:

- If `CONTEXT-MAP.md` exists, read it to find contexts and their relationships
- Create more `0001-CONTEXT-slug.md` lazily when the term is resolved

When multiple contexts exist, infer which one the current topic relates to. If unclear, ask.
