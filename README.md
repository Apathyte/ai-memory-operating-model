# AI Memory Operating Model

I dumped the persistent context I had built up with an AI assistant.

Some of it was governance.
Some of it was useful operating context.
Some of it was preference.
Some of it had absolutely no business being persistent.

So I classified it.

This repository is a small operating pattern for deciding **what deserves to persist, what should expire, what should be removed, and which items need explicit human authority around them**.

It is not a universal AI-governance framework, and it is not an implementation of a memory store.

## Scope

This repo is about **governing persistent assistant context**.

It does **not** provide:
- vector retrieval
- semantic search
- TTL engines
- automated pruning
- database-backed long-term memory
- policy middleware
- production enforcement infrastructure

Those are implementation concerns. This repo focuses on the decision layer that should exist before or alongside them.

## Two axes, not one

The original mistake was treating everything in one table as if it belonged to one taxonomy.

It does not.

### Class
`Class` answers:

> What kind of persistent context is this?

| Class | Meaning | Default treatment |
|---|---|---|
| Governance | Rules the assistant should obey | Keep deliberately |
| Operating Context | Facts needed to do useful work | Keep while relevant |
| Preference | Stable ways the human prefers to work | Keep when genuinely useful |
| Ephemera | Short-lived or low-value residue | Remove or let expire |

### Function
`Function` answers:

> What does this item concern?

Examples include governance, security, writing, architecture, delivery, or AI behaviour.

A memory item can therefore be:

- `Class = Governance`
- `Function = Security`

without contradiction.

## Persistence states

Every item should also receive a persistence decision:

| State | Meaning |
|---|---|
| Keep | Stable enough and useful enough to persist |
| Temporary | Useful now, but should expire or be reviewed |
| Remove | Persistence is not justified |

## Eight controls we chose to highlight

These are **not the entire dataset**. They are the clearest reusable controls from the surviving governance layer.

1. **Human authority**  
   Availability of a tool is not permission to use it.

2. **Preservation**  
   An improvement that destroys information is not automatically an improvement.

3. **Provenance**  
   Never invent where a fact, decision, or execution came from.

4. **Evidence**  
   Retrieve approved material before reconstructing it from memory.

5. **Uncertainty**  
   Unknown authority means stop, not infer permission.

6. **Privacy**  
   Operationally useful does not automatically mean appropriate for persistent memory.

7. **Minimisation**  
   Short-lived context should not quietly become identity.

8. **Separation**  
   Governance, facts, preferences, and transient context are different classes.

## Core controls vs principles worth persisting

The repo deliberately keeps two different outputs separate.

[`sanitised-memory.md`](sanitised-memory.md) contains the **memory-governance core**: controls directly related to persistence, authority, privacy, provenance, evidence, retrieval, capability honesty, and consequential action.

[`principles-worth-persisting.md`](principles-worth-persisting.md) contains **sanitised examples of useful non-core principles that survived the same classification process**. These include things like `HARD / INFER / UNKNOWN`, operational truth, authority mapping, security-before-joke, and other stable working principles.

That separation is intentional:

> The model decides what deserves persistence. The companion file shows examples of the kind of value that may survive that decision.

This keeps the taxonomy clean without throwing away useful context simply because it is not itself a memory-governance control.

## Worked examples

See [`classification-examples.md`](classification-examples.md).

That file shows the actual method:

`raw memory → assessment → class → persistence decision → public form`

It includes examples of:
- a governance rule that should remain
- customer-specific operating context that should not remain in raw form
- one-off ephemera that should be removed

## Enforcement

Prompt text is not a security boundary.

For lightweight personal workflows, a rule can live in persistent assistant context.

For consequential production systems, hard constraints should be enforced in application logic, permissions, middleware, policy checks, or approval gates.

See [`enforcement-example.md`](enforcement-example.md).

## Use it

1. Export or review the persistent context your assistant is using.
2. Remove secrets and obviously sensitive material before sharing anything.
3. Assign each item a `Class`.
4. Assign its `Function`.
5. Decide `Keep`, `Temporary`, or `Remove`.
6. Add an expiry/review condition where needed.
7. Distill private operating context into reusable principles where appropriate.
8. Put consequential rules behind real enforcement where consequences justify it.
9. Re-run the review periodically.

A blank template is included in [`memory-template.md`](memory-template.md).

## Privacy warning

**Do not publish a raw memory dump.**

Useful memory can still contain:
- personal information
- customer-identifying detail
- internal politics
- security-adjacent facts
- infrastructure details
- accidental mosaics that identify people or organisations when combined

Sanitise first. Publish second.

## What this is not

This is not:
- a claim that these exact rules are correct for everyone
- a complete AI policy framework
- a memory database architecture
- a substitute for production security controls

It is a practical pattern:

**inspect → classify → minimise → retain / expire / remove → govern**

## License

MIT License. See [`LICENSE`](LICENSE).
