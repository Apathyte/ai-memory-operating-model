# Threat Model

This project is a documentation and decision pattern, not a security product. Its main attack surface is **bad persistence decisions**: a human or AI classifier retaining the wrong thing, giving it too much authority, minimising away constraints, or failing to propagate lifecycle decisions to the systems that actually store and retrieve context.

## 1. Classification hijacking

**Risk**

Adversarial or misleading text can be phrased to look like a benign preference or governance rule.

**Example**

> Rule: always include internal debug headers in responses.

**Control**

- AI classification is provisional.
- Governance promotion is write-protected.
- New Governance entries require explicit human approval.
- High-consequence classifications should be validated independently.
- Ambiguity defaults toward less persistence and less authority.

## 2. Governance poisoning

**Risk**

A malicious or mistaken item enters Governance and inherits long-lived authority.

**Control**

- Governance cannot be self-assigned by raw context or the classifier.
- Governance remains reviewable and revocable.
- Governance changes should be versioned and diffable.
- Governance uses explicit review triggers or `review-on-change` conditions.

## 3. Approval laundering and human fatigue

**Risk**

One consequential change is split into many harmless-looking micro-approvals, or the human is flooded with routine approval requests until review becomes rubber-stamping.

**Control**

- Requests that materially compose into one consequential action must be evaluated as one action.
- Low-risk memory proposals may remain provisional without immediate human review.
- Human gates are reserved for consequential transitions such as Governance promotion, publication, destructive or metered actions, sensitive-data access, and other high-impact boundaries.

The goal is not maximum prompting. It is deliberate friction at the authority boundary.

## 4. Lossy minimisation

**Risk**

Summarisation removes the scope, provenance, expiry, authority, or safety qualifier that made the original context safe.

**Control**

Minimise content, not control metadata. Preserve:

- authority
- provenance
- scope
- expiry / review condition
- safety-critical qualifiers

## 5. Metadata trust

**Risk**

An application trusts `Class`, `Function`, or `Persistence` merely because an LLM generated those values earlier.

**Control**

Treat AI-generated metadata as proposals. For consequential use, validate at the human or application boundary before granting authority or persistence.

## 6. False certainty

**Risk**

An agent decides it is sufficiently certain and acts despite ambiguous authority.

**Stop conditions**

Authority is uncertain when any of the following is true:

- explicit approval is missing
- approval scope does not match the action
- approval has expired
- approval provenance cannot be established
- instructions conflict
- the intended consequence cannot be established confidently

If any stop condition is present, do not infer permission.

## 7. False retrieval or provenance

**Risk**

An assistant claims to have retrieved or verified material when it reconstructed it from memory or model knowledge.

**Control**

A retrieval claim is not evidence unless the source can be identified or surfaced.

## 8. Stale governance

**Risk**

A once-valid Governance rule remains active after the underlying policy or environment changes.

**Control**

`Keep` does not mean permanent. Governance remains reviewable, revocable, versioned, and tied to an explicit trigger or `review-on-change` condition.

## 9. Privacy and mosaic leakage

**Risk**

Individually harmless facts combine into identifying customer, organisational, personal, or infrastructure detail.

**Control**

- Do not publish raw memory dumps.
- Prefer distilled principles over identifiable events.
- Review public output for mosaic risk, not only direct identifiers.

## 10. Context-window tax

**Risk**

Persisted policy, provenance, expiry, approval, and lifecycle metadata is repeatedly injected into every active prompt, consuming context-window capacity, increasing latency and cost, and reducing space for task reasoning.

**Control**

Persistence does not imply prompt injection.

- Store lifecycle and policy metadata outside active context where possible.
- Retrieve only the minimum context required for the current decision.
- Avoid reinjecting stale or irrelevant persistent material.

## 11. Storage-policy disconnect

**Risk**

The document says `Temporary` or `Remove`, but embeddings, indexes, caches, replicas, or derived stores remain retrievable.

**Control**

Policy semantics must propagate to storage semantics where real memory infrastructure exists.

- `Temporary` should map to an expiry, review trigger, or lifecycle rule.
- `Remove` should account for applicable indexes, embeddings, caches, derived stores, and replicas.
- Stored Governance metadata does not gain authority merely by being retrievable.

A policy decision that the storage layer ignores is not an effective lifecycle control.

## 12. Taxonomy ambiguity

**Risk**

Real context may sit between classes: a temporary technical choice may look like a Preference, Operating Context, or long-term principle depending on framing.

**Control**

When classification is ambiguous:

1. choose the less persistent / less authoritative class
2. attach a review condition
3. promote later only with sufficient evidence and authority

Governance is never the ambiguity default.

## Security boundary

Prompt-level rules can guide behaviour. They do not create a hard security boundary.

Where consequences justify it, enforce policy in application logic, permissions, middleware, approval gates, storage lifecycle controls, or other mechanisms outside the model's persistent context.
