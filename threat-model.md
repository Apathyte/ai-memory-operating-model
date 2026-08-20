# Threat Model

This project is a documentation and decision pattern, not a security product. Its main attack surface is **bad persistence decisions**: a human or AI classifier retaining the wrong thing, giving it too much authority, or minimising away the constraints that made it safe.

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

## 2. Governance poisoning

**Risk**

A malicious or mistaken item enters Governance and inherits long-lived authority.

**Control**

- Governance cannot be self-assigned by raw context or the classifier.
- Governance remains reviewable and revocable.
- Governance changes should be versioned and diffable.

## 3. Approval laundering

**Risk**

One consequential change is split into many harmless-looking micro-approvals until the human gate becomes routine.

**Control**

Requests that materially compose into one consequential action must be evaluated as one action.

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

`Keep` does not mean permanent. Governance remains reviewable, revocable, and versioned.

## 9. Privacy and mosaic leakage

**Risk**

Individually harmless facts combine into identifying customer, organisational, personal, or infrastructure detail.

**Control**

- Do not publish raw memory dumps.
- Prefer distilled principles over identifiable events.
- Review public output for mosaic risk, not only direct identifiers.

## Security boundary

Prompt-level rules can guide behaviour. They do not create a hard security boundary.

Where consequences justify it, enforce policy in application logic, permissions, middleware, approval gates, or other controls outside the model's persistent context.
