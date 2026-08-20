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

It does **not** provide vector retrieval, semantic search, TTL engines, automated pruning, database-backed long-term memory, policy middleware, or production enforcement infrastructure.

Those are implementation concerns. This repo focuses on the decision and authority layer that should exist before or alongside them.

## The core flow

The model deliberately separates three different acts:

**PROPOSE → VALIDATE → AUTHORISE**

- **Propose:** a human or AI may suggest a `Class`, `Function`, and `Persistence` decision.
- **Validate:** check sensitivity, provenance, ambiguity, scope, expiry, and whether the proposal is adversarial or over-authoritative.
- **Authorise:** only the appropriate human or application boundary may grant consequential persistence or Governance authority.

Classification is not authority.

## Two axes, not one

### Class

`Class` answers:

> What kind of persistent context is this?

| Class | Meaning | Default treatment |
|---|---|---|
| Governance | Rules the assistant should obey | Human-approved, versioned, reviewable |
| Operating Context | Facts needed to do useful work | Keep while relevant |
| Preference | Stable ways the human prefers to work | Keep when genuinely useful |
| Ephemera | Short-lived or low-value residue | Remove or let expire |

### Function

`Function` answers:

> What does this item concern?

Examples include governance, security, writing, architecture, delivery, or AI behaviour.

`Function` is descriptive metadata, not an authority or trust signal.

## Persistence states

| State | Meaning |
|---|---|
| Keep | Stable enough and useful enough to persist, subject to review |
| Temporary | Useful now, but should expire or be reviewed |
| Remove | Persistence is not justified |

`Keep` does not mean permanent or unquestionable.

## Ambiguity defaults downward

The taxonomy is intentionally practical, not mathematically perfect.

When an item plausibly fits more than one class, choose the **less persistent / less authoritative** option and attach a review condition.

Examples:

- Preference vs Operating Context → prefer Operating Context if it may only be true for the current project.
- Operating Context vs Ephemera → prefer Ephemera if future value cannot be justified.
- Anything vs Governance → Governance requires explicit promotion; it is never the default.

## Governance is write-protected

Governance has authority, so promotion into Governance must itself be governed.

- Raw context, Operating Context, Preferences, and Ephemera **must not be promoted automatically into Governance**.
- New Governance entries require explicit human approval.
- AI-generated `Class`, `Function`, and `Persistence` values are proposals, not trusted policy metadata.
- Governance entries remain reviewable and revocable.
- Governance changes should be versioned and diffable rather than silently replaced.

## Provisional fast path, authoritative slow path

Human review should not be required for every low-risk memory proposal.

Low-risk context may remain **provisional** until one of these boundaries is crossed:

- promotion into Governance
- consequential use
- publication
- access to sensitive or customer data
- destructive or metered action
- a transition from Temporary to Keep where the consequence matters

This preserves useful autonomy without laundering authority through convenience.

Fragmented requests that materially compose into one consequential action are evaluated as one action.

## Persistence does not mean prompt injection

Stored context does not need to occupy every active prompt.

Where possible:

- keep policy and lifecycle metadata outside the active context
- retrieve only the minimum context required for the current decision
- avoid repeatedly injecting stale or irrelevant persistent material

The model governs **what may persist and with what authority**. It does not require all persistent material to be continuously loaded into the model context.

## Policy semantics must reach storage semantics

A persistence decision is incomplete if the storage layer ignores it.

Where a real memory infrastructure exists:

- `Temporary` should map to an expiry, review trigger, or lifecycle rule
- `Remove` should account for applicable indexes, embeddings, caches, derived stores, and replicas
- Governance metadata should not inherit authority merely because it exists in storage

A document-level `Remove` decision that leaves retrievable derived copies behind is not meaningful removal.

## Review triggers, not review theatre

Governance should be reviewable without creating arbitrary calendar churn.

Each Governance entry should have either:

- an explicit review trigger, or
- a `review-on-change` condition tied to the underlying policy, system, authority, or environment

Event-driven review is usually preferable to repeatedly asking humans to reconfirm unchanged rules.

## Hardening rules

1. **Governance is write-protected** — authority cannot be self-assigned by the classifier.
2. **Governance remains reviewable** — `Keep` does not mean forever or beyond challenge.
3. **Fragmented approvals compose** — micro-requests that form one consequential action are assessed together.
4. **Minimise content, preserve control metadata** — never compress away authority, provenance, scope, expiry, or safety qualifiers.
5. **AI classification is a proposal** — high-consequence classification needs independent validation.
6. **Uncertainty has concrete triggers** — missing, mismatched, expired, conflicting, unverifiable authority or unclear consequences means stop.
7. **Governance changes are auditable** — prefer visible diffs and approval trails over silent mutation.
8. **Ambiguity defaults downward** — when unsure, choose less persistence and less authority.
9. **Persistence ≠ prompt injection** — store broadly only when justified; retrieve narrowly when needed.
10. **Storage must honour policy semantics** — expiry and removal must propagate to the stores that can still retrieve the item.

## Eight controls we chose to highlight

These remain a curated subset of the broader governance layer:

1. Human authority
2. Preservation
3. Provenance
4. Evidence
5. Uncertainty
6. Privacy
7. Minimisation
8. Separation

## Core controls vs principles worth persisting

[`sanitised-memory.md`](sanitised-memory.md) contains the **memory-governance core**.

[`principles-worth-persisting.md`](principles-worth-persisting.md) contains **sanitised examples of useful non-core principles that survived the same classification process**, including `HARD / INFER / UNKNOWN`, operational truth, authority mapping, security-before-joke, and other stable working principles.

> The model decides what deserves persistence. The companion file shows examples of the kind of value that may survive that decision.

## Worked examples

See [`classification-examples.md`](classification-examples.md).

The method is:

`raw context → proposed class/function → validate → persistence decision → minimise → authorise → review`

## Enforcement

Prompt text is not a security boundary.

For lightweight personal workflows, rules can live in persistent assistant context as behavioural guidance.

For consequential production systems, hard constraints should be enforced in application logic, permissions, middleware, policy checks, storage lifecycle controls, or approval gates.

Stored `Class` or `Persistence` metadata should not be trusted merely because an LLM generated it.

See [`enforcement-example.md`](enforcement-example.md).

## Adversarial model

See [`threat-model.md`](threat-model.md) for the explicit failure modes this pattern is designed to resist, including classification hijacking, governance poisoning, approval laundering, lossy minimisation, metadata trust, stale governance, human review fatigue, context-window tax, infrastructure-policy drift, and taxonomy ambiguity.

## Use it

1. Export or review the persistent context your assistant is using.
2. Remove secrets and obviously sensitive material before sharing anything.
3. Assign each item a proposed `Class`.
4. Assign its descriptive `Function`.
5. Validate sensitivity, provenance, ambiguity, authority, and scope.
6. Decide `Keep`, `Temporary`, or `Remove`.
7. If proposed as Governance, require explicit human approval.
8. If classification is ambiguous, default downward and attach a review condition.
9. Add an expiry or review trigger where needed.
10. Distill private operating context into reusable principles where appropriate.
11. During minimisation, preserve authority, provenance, scope, expiry, and safety qualifiers.
12. Do not inject persistent material into active context unless it is needed for the current task.
13. Put consequential rules behind real enforcement where consequences justify it.
14. Ensure storage lifecycle mechanics honour Temporary and Remove decisions.
15. Review changes as diffs rather than silent replacements.
16. Re-run review when a trigger fires or the underlying context changes.

A blank template is included in [`memory-template.md`](memory-template.md).

## Privacy warning

**Do not publish a raw memory dump.**

Useful memory can still contain personal information, customer-identifying detail, internal politics, security-adjacent facts, infrastructure details, or accidental mosaics that identify people or organisations when combined.

Sanitise first. Publish second.

## What this is not

This is not:

- a claim that these exact rules are correct for everyone
- a complete AI policy framework
- a memory database architecture
- a substitute for production security controls
- a claim that prompt-level memory rules can enforce themselves
- a requirement to inject all persistent context into every prompt

It is a practical pattern:

**inspect → propose → validate → minimise → retain / expire / remove → authorise → review**

## License

MIT License. See [`LICENSE`](LICENSE).
