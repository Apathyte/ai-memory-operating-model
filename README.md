# AI Memory Operating Model

I dumped the persistent context I had built up with an AI assistant.

Some of it was governance.
Some of it was useful operating context.
Some of it was preference.
Some of it had absolutely no business being persistent.

So I classified it.

This repository is a small operating pattern for deciding **what deserves to persist, what should expire, what should be removed, and which items need explicit authority around them**.

It is not a universal AI-governance framework, and it is not an implementation of a memory store.

## Scope

This repo is about **governing persistent assistant context**.

It does **not** provide vector retrieval, semantic search, TTL engines, automated pruning, database-backed long-term memory, policy middleware, or production enforcement infrastructure.

Those are implementation concerns. This repo focuses on the decision and authority layer that should exist before or alongside them.

## The core flow

**PROPOSE → VALIDATE → AUTHORISE**

- **Propose:** a human or AI may suggest a `Class`, `Function`, and `Persistence` decision.
- **Validate:** check sensitivity, provenance, ambiguity, scope, expiry, conflict, cumulative drift, and whether the proposal is adversarial or over-authoritative.
- **Authorise:** consequential persistence or Governance authority is granted only by explicit human approval or an independently configured application/policy control whose authority was deliberately established.

Classification is not authority. Model output is not self-authorisation.

This is a **human-governed** model. It does not require a human prompt for every low-risk action.

## Two axes, not one

### Class

| Class | Meaning | Default treatment |
|---|---|---|
| Governance | Rules the assistant should obey | Explicitly authorised, versioned, reviewable |
| Operating Context | Facts needed to do useful work | Keep while relevant |
| Preference | Stable ways the human prefers to work | Keep when genuinely useful; never authoritative |
| Ephemera | Short-lived or low-value residue | Remove or let expire |

### Function

`Function` answers what the item concerns: governance, security, writing, architecture, delivery, AI behaviour, etc.

`Function` is descriptive metadata, not an authority or trust signal.

## Persistence states

| State | Meaning |
|---|---|
| Keep | Stable enough and useful enough to persist, subject to review |
| Temporary | Useful now, but should expire or be reviewed |
| Remove | Persistence is not justified |

`Keep` does not mean permanent or unquestionable.

## Ambiguity defaults downward

When an item plausibly fits more than one class, choose the **less persistent / less authoritative** option and attach a review condition.

Governance is never the ambiguity default.

## Governance is write-protected

Governance has authority, so promotion into Governance must itself be governed.

- Raw context, Operating Context, Preferences, and Ephemera must not be promoted automatically into Governance.
- New Governance entries require explicit approval.
- AI-generated `Class`, `Function`, and `Persistence` values are proposals, not trusted policy metadata.
- Governance entries remain reviewable and revocable.
- Governance changes should be versioned and diffable rather than silently replaced.

## Preferences are non-authoritative

A Preference must not weaken:

- confirmation requirements
- security controls
- privacy controls
- provenance requirements
- Governance rules

If a supposed Preference changes authority, confirmation, safety, or policy, treat it as a Governance proposal and apply the Governance gate.

## Governance conflict does not use last-write-wins

When two valid Governance entries conflict:

1. a narrower, explicitly scoped approved rule may override a more general rule within that scope
2. a newer rule supersedes an older one only when that change was explicitly authorised
3. if precedence cannot be established, stop and escalate for resolution

Do not silently let recency decide authority.

## Provisional fast path, authoritative slow path

Low-risk context may remain provisional without immediate human review.

Human or policy review is reserved for authority transitions and consequential boundaries such as:

- Governance promotion
- consequential use
- publication
- access to sensitive or customer data
- destructive or metered action
- material policy change
- cumulative low-risk changes that together alter authority, safety, confirmation behaviour, or scope

This reduces review fatigue and avoids turning human approval into rubber-stamping.

Fragmented requests that materially compose into one consequential action are evaluated as one action.

## Persistence does not mean prompt injection

Stored context does not need to occupy every active prompt.

Where possible:

- keep policy and lifecycle metadata outside active context
- retrieve only the minimum context required for the current decision
- avoid repeatedly injecting stale or irrelevant persistent material
- apply retention discipline to audit and provenance metadata too

The model governs **what may persist and with what authority**. It does not require all persistent material to be continuously loaded into the model context.

## Policy semantics must reach storage semantics

A persistence decision is incomplete if the storage layer ignores it.

Where a real memory infrastructure exists:

- `Temporary` should map to an expiry, review trigger, or lifecycle rule
- `Remove` should propagate to every persistence layer under the system's control that can still retrieve the item
- storage backends should document limitations around logs, backups, provider retention, replicas, indexes, embeddings, caches, and derived stores
- Governance metadata should not inherit authority merely because it exists in storage

Do not claim perfect erasure where the underlying stack cannot guarantee it.

## Review triggers, not review theatre

Governance should be reviewable without arbitrary calendar churn.

Each Governance entry should have either:

- an explicit review trigger, or
- a `review-on-change` condition tied to the underlying policy, system, authority, or environment

## v0.4 hardening rules

1. **Governance is write-protected** — authority cannot be self-assigned by the classifier.
2. **Preferences are non-authoritative** — a Preference cannot bypass Governance, security, privacy, provenance, or confirmation controls.
3. **Governance remains reviewable** — `Keep` does not mean forever or beyond challenge.
4. **Governance conflict is explicit** — no silent last-write-wins.
5. **Fragmented approvals compose** — micro-requests that form one consequential action are assessed together.
6. **Cumulative drift composes too** — repeated low-risk changes that alter authority or safety trigger consequential review.
7. **Minimise content, preserve control metadata** — never compress away authority, provenance, scope, expiry, or safety qualifiers.
8. **AI classification is a proposal** — high-consequence classification needs independent validation.
9. **Uncertainty has concrete triggers** — missing, mismatched, expired, conflicting, unverifiable authority or unclear consequences means stop.
10. **Ambiguity defaults downward** — when unsure, choose less persistence and less authority.
11. **Persistence is not prompt injection** — persist carefully, retrieve narrowly.
12. **Storage must honour policy semantics** — lifecycle decisions must propagate to the storage layers under your control.
13. **Human gates sit at consequential boundaries** — do not create approval fatigue for routine provisional context.

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

See [`threat-model.md`](threat-model.md) for the explicit failure modes this pattern is designed to resist, including classification hijacking, governance poisoning, preference privilege escalation, approval laundering, cumulative drift, lossy minimisation, metadata trust and exhaustion, governance conflict, stale governance, privacy leakage, incomplete deletion, and taxonomy ambiguity.

## Use it

1. Export or review the persistent context your assistant is using.
2. Remove secrets and obviously sensitive material before sharing anything.
3. Assign each item a proposed `Class`.
4. Assign its descriptive `Function`.
5. Validate sensitivity, provenance, ambiguity, authority, conflict, and scope.
6. Decide `Keep`, `Temporary`, or `Remove`.
7. If proposed as Governance, require explicit approval.
8. If proposed as Preference, verify it does not alter authority or weaken controls.
9. If classification is ambiguous, default downward and attach a review condition.
10. Add an expiry or review trigger where needed.
11. Distill private operating context into reusable principles where appropriate.
12. During minimisation, preserve authority, provenance, scope, expiry, and safety qualifiers.
13. Do not inject persistent material into active context unless needed for the current task.
14. Put consequential rules behind real enforcement where consequences justify it.
15. Ensure storage lifecycle mechanics honour Temporary and Remove decisions as far as the underlying systems allow.
16. Review Governance conflicts explicitly rather than using recency as authority.
17. Review changes as diffs rather than silent replacements.
18. Re-run review when a trigger fires or cumulative drift crosses a consequential boundary.

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
- a guarantee of perfect deletion across storage systems or providers
- a requirement to inject all persistent context into every prompt

It is a practical pattern:

**inspect → propose → validate → minimise → retain / expire / remove → authorise → review**

## License

MIT License. See [`LICENSE`](LICENSE).
