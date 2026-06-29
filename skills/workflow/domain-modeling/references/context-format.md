# CONTEXT.md Format

## Structure

```md
# {Context Name}

{One or two sentence description of what this context is and why it exists.}

## Language

### Area Name (optional)

**Term**:
{A short but sufficiently detailed description of the term}
_Avoid_: Synonyms
```

Example:

```md
### Core Concepts

**Customer**:
A person or organization that places **Orders**.
_Avoid_: Client, Buyer, Account

**Order**:
A request for goods or services placed by a **Customer**.
_Avoid_: Purchase, Transaction

**Invoice**:
A request for payment sent to a **Customer** after an **Order** is fulfilled.
_Avoid_: Bill, Payment Request

### Videos and Clips

**Video**:
A container of **Clips** and **Chapters** that represents a single producible video output.
_Avoid_: Recording, Movie

**Reference Video**:
Another **Video** on the same **Lesson**, opened alongside the one being recorded so the author can read its **Clip** transcripts grouped by **Chapter** while re-recording. Not a domain link; the candidate set is derived as other non-archived **Videos** on this **Lesson**.
_Avoid_: Previous Take, Reference Take, Source Video
```

## Rules

- **Be opinionated.** When multiple words exist for the same concept, pick the best one and list the others under `_Avoid_`.
- **Keep definitions short but sufficiently detailed.** Define what the term is, including only explicitly resolved information that is useful as long-term source of truth. A term can grow over time as more durable meaning is resolved, but every sentence must earn its place.
- **`CONTEXT.md` is for canonical domain language only.** Relationships, examples, and resolved ambiguities live fluently inside the relevant term description or `_Avoid_` line, not in separate sections.
- **Bold domain term references.** When a term description references another domain term from the `CONTEXT.md`, write it in bold, for example `**Video**` or `**Clip**`.
- **Only include terms specific to this project's context.** General programming concepts (timeouts, error types, utility patterns) don't belong even if the project uses them extensively. Before adding a term, ask: is this a concept unique to this context, or a general programming concept? Only the former belongs.
- **Do not turn `CONTEXT.md` into a spec.** Only include inline code, storage, UI, or workflow facts when they are explicitly resolved and necessary to prevent a durable misunderstanding of the term.
- **Group terms under subheadings when natural clusters emerge.** If all terms belong to a single cohesive area, a flat list is fine.
- **Use existing structure when present.** Do not churn an established `CONTEXT.md` just to match this template.

## Single vs multi-context repos

**Single context (most repos):** One `CONTEXT.md` at the repo root.

**Multiple contexts:** A `CONTEXT-MAP.md` at the repo root lists the contexts, where they live, and how they relate to each other:

```md
# Context Map

## Contexts

- [Ordering](./src/ordering/CONTEXT.md) - receives and tracks customer orders
- [Billing](./src/billing/CONTEXT.md) - generates invoices and processes payments
- [Fulfillment](./src/fulfillment/CONTEXT.md) - manages warehouse picking and shipping

## Relationships

- **Ordering → Fulfillment**: Ordering emits `OrderPlaced` events; Fulfillment consumes them to start picking
- **Fulfillment → Billing**: Fulfillment emits `ShipmentDispatched` events; Billing consumes them to generate invoices
- **Ordering ↔ Billing**: Shared types for `CustomerId` and `Money`
```

The skill infers which structure applies:

- If `CONTEXT-MAP.md` exists, read it to find contexts
- If only a root `CONTEXT.md` exists, single context
- If neither exists, create a root `CONTEXT.md` lazily when the first term is resolved

When multiple contexts exist, infer which one the current topic relates to. If unclear, ask.
