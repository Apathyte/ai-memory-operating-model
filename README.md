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

## Governance is write-protected

Governance has authority, so promotion into Governance must itself be governed.

- Raw context, Operating Context, Preferences, and Ephemera **must not be promoted automatically into Governance**.
- New Governance entries require explicit human approval.
- AI-generated `Class`, `Function`, and `Persistence` values are proposals, not trusted policy metadata.
- Governance entries must remain reviewable and revocable.
- Governance changes should be versioned and diffable rather than silently replaced.

## Seven hardening rules

1. **Governance is write-protected**  
   Authority cannot be self-assigned by the classifier.

2. **Governance remains reviewable**  
   `Keep` does not mean forever or beyond challenge.

3. **Fragmented approvals compose**  
   Multiple small requests that materially form one consequential action must be assessed as one action.

4. **Minimise content, preserve control metadata**  
   Minimisation must not discard authority, provenance, scope, expiry, or safety-critical qualifiers.

5. **AI classification is a proposal**  
   High-consequence classification needs independent human or application-side validation.

6. **Uncertainty has concrete triggers**  
   Stop when approval is missing, out of scope, expired, conflicting, unverifiable, or consequences cannot be established confidently.

7. **Governance changes are auditable**  
   Prefer a visible diff and approval trail over silent mutation.

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

`raw memory → assessment → class → function → persistence decision → public/minimised form`

## Enforcement

Prompt text is not a security boundary.

For lightweight personal workflows, a rule can live in persistent assistant context.

For consequential production systems, hard constraints should be enforced in application logic, permissions, middleware, policy checks, or approval gates.

Stored `Class` or `Persistence` metadata should not be trusted merely because an LLM generated it.

See [`enforcement-example.md`](enforcement-example.md).

## Adversarial model

See [`threat-model.md`](threat-model.md) for the explicit failure modes this pattern is designed to resist, including classification hijacking, governance poisoning, approval laundering, lossy minimisation, metadata trust, and stale governance.

## Use it

1. Export or review the persistent context your assistant is using.
2. Remove secrets and obviously sensitive material before sharing anything.
3. Assign each item a proposed `Class`.
4. Assign its `Function`.
5. Decide `Keep`, `Temporary`, or `Remove`.
6. If proposed as Governance, require explicit human approval.
7. Add an expiry or review condition where needed.
8. Distill private operating context into reusable principles where appropriate.
9. During minimisation, preserve authority, provenance, scope, expiry, and safety qualifiers.
10. Put consequential rules behind real enforcement where consequences justify it.
11. Review changes as diffs rather than silent replacements.
12. Re-run the review periodically.

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

It is a practical pattern:

**inspect → classify → validate → minimise → retain / expire / remove → govern → review**

## License

MIT License. See [`LICENSE`](LICENSE).
