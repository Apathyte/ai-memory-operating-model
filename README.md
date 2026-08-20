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

It does **not** provide vector retrieval, semantic search, TTL engines, automated pruning, database-backed long-term memory, policy middleware, RBAC, or production enforcement infrastructure.

Those are implementation concerns. This repo focuses on the decision, lifecycle, and authority semantics that should exist before or alongside them.

## The core flow

**PROPOSE → VALIDATE → AUTHORISE**

- **Propose:** a human or AI may suggest a `Class`, `Function`, and `Lifecycle` decision.
- **Validate:** check sensitivity, provenance, ambiguity, scope, expiry, conflict, cumulative drift, and whether the proposal is adversarial or over-authoritative.
- **Authorise:** consequential persistence or Governance authority is granted only by explicit human approval or by a policy/application control whose authority and independence were deliberately established.

Classification is not authority. Model output is not self-authorisation.

This is a **human-governed** model. It does not require a human prompt for every low-risk action.

## Four classes of context

| Class | Meaning | Default treatment |
|---|---|---|
| Governance | Rules the assistant should obey | Explicitly authorised, versioned, reviewable |
| Operating Context | Facts needed to do useful work | Keep while relevant |
| Preference | Stable ways the human prefers to work | Keep when genuinely useful; never authoritative |
| Ephemera | Short-lived or low-value residue | Remove or let expire |

`Function` is a separate descriptive tag for what the item concerns: governance, security, writing, architecture, delivery, AI behaviour, etc. It is not an authority signal.

## Lifecycle states

| State | Meaning |
|---|---|
| Keep | Stable enough and useful enough to persist, subject to review |
| Temporary | Useful now, but must expire, renew explicitly, or be re-evaluated |
| Remove | Persistence is not justified |

`Keep` does not mean permanent or unquestionable.

## Ambiguity defaults downward

When an item plausibly fits more than one class, choose the **less persistent / less authoritative** option and attach a review condition.

Governance is never the ambiguity default.

## Governance is write-protected

Governance has authority, so promotion into Governance must itself be governed.

- Raw context, Operating Context, Preferences, and Ephemera must not be promoted automatically into Governance.
- New Governance entries require explicit approval.
- AI-generated `Class`, `Function`, and `Lifecycle` values are proposals, not trusted policy metadata.
- Governance entries remain reviewable and revocable.
- Governance changes should be versioned and diffable rather than silently replaced.

## Non-Governance can inform, not authorise

A classification label does not neutralise the token-level influence of context once that context is presented to a model.

The semantic boundary is therefore stronger than the label:

> **Only Governance may grant or modify authority. Non-Governance context may inform reasoning, but it must not grant permission, weaken controls, change confirmation requirements, override Governance, or become authoritative merely because it appears in active context.**

Where the platform allows it, keep untrusted or provisional context structurally separate from policy/control instructions. Retrieved memory should be treated as data unless it has passed the authority path required to become Governance.

Do not convert retrieved context into privileged instructions merely by concatenating it into a prompt.

## Preferences are non-authoritative

A Preference must not weaken confirmation, security, privacy, provenance, or Governance controls.

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

Fragmented requests that materially compose into one consequential action are evaluated as one action.

Repeated low-risk changes that cumulatively change authority or safety are treated as one consequential transition.

## Temporary does not renew itself into permanence

Temporary context may be renewed, but repeated renewal must not silently create de facto `Keep` status.

Each implementation should define a forcing function such as a maximum cumulative duration, renewal count, material scope change, or repeated use beyond the original purpose. When that trigger fires, the item becomes a fresh lifecycle decision.

Temporary authority does not compound into permanent authority by neglect.

## Independence is a trust boundary

"Independent policy control" is not a magic phrase.

An automated validator or authoriser is independent only when the proposing model or workflow cannot unilaterally alter the mechanism that validates or authorises its proposal.

That may be implemented through separate credentials, permission scope, deployment paths, approval state, policy configuration, or another trust boundary appropriate to the system.

The invariant is simple:

> the proposer must not control the thing that grants it authority.

See [`authority-boundaries.md`](authority-boundaries.md).

## Evidence must not prove itself

AI-authored reasoning can explain a proposal. It is not independent evidence for granting authority.

Consequential promotion should rely on identifiable source material, logs, approved policy records, authenticated decisions, independently generated application signals, or explicit human judgement.

A model-generated justification can accompany evidence. It cannot be its own proof.

## Recursive governance

Changes to the model's own Governance rules should pass through the same discipline they impose on governed context:

**PROPOSE → VALIDATE → AUTHORISE → VERSION → REVIEW**

A component proposing a governance change must not be able to unilaterally modify the mechanism that validates or authorises that same change.

A diff is evidence that something changed. It is not proof that the change was properly authorised.

## Persistence does not mean prompt injection

Stored context does not need to occupy every active prompt.

Where possible:

- keep policy and lifecycle metadata outside active context
- retrieve only the minimum context required for the current decision
- avoid repeatedly injecting stale or irrelevant persistent material
- apply retention discipline to audit and provenance metadata too

## Policy semantics must reach storage semantics

A lifecycle decision is incomplete if the storage layer ignores it.

Where real memory infrastructure exists:

- `Temporary` should map to expiry, renewal, review, or lifecycle rules
- `Remove` should propagate to every persistence layer under the system's control that can still retrieve the item
- storage backends should document limitations around logs, backups, provider retention, replicas, indexes, embeddings, caches, and derived stores
- Governance metadata should not inherit authority merely because it exists in storage

Do not claim perfect erasure where the underlying stack cannot guarantee it.

## Review triggers, not review theatre

Each Governance entry should have either an explicit review trigger or a `review-on-change` condition tied to the underlying policy, system, authority, or environment.

Event-driven review is usually preferable to arbitrary calendar churn.

## v0.5 hardening rules

1. **Governance is write-protected** — authority cannot be self-assigned by the classifier.
2. **Preferences are non-authoritative** — a Preference cannot bypass Governance, security, privacy, provenance, or confirmation controls.
3. **Non-Governance can inform, not authorise** — context does not gain authority merely by entering the model's active context.
4. **Governance remains reviewable** — `Keep` does not mean forever or beyond challenge.
5. **Governance conflict is explicit** — no silent last-write-wins.
6. **Fragmented approvals compose** — micro-requests that form one consequential action are assessed together.
7. **Cumulative drift composes too** — repeated low-risk changes that alter authority or safety trigger consequential review.
8. **Temporary renewal is bounded** — repeated renewal must eventually force a fresh lifecycle decision.
9. **Minimise content, preserve control metadata** — never compress away authority, provenance, scope, expiry, or safety qualifiers.
10. **AI classification is a proposal** — consequential classification needs independent validation.
11. **Evidence cannot self-attest** — model-generated justification is not independent evidence for authority.
12. **Uncertainty has concrete triggers** — missing, mismatched, expired, conflicting, unverifiable authority or unclear consequences means stop.
13. **Ambiguity defaults downward** — when unsure, choose less persistence and less authority.
14. **Persistence is not prompt injection** — persist carefully, retrieve narrowly.
15. **Storage must honour lifecycle semantics** — lifecycle decisions must propagate to storage layers under your control.
16. **Human gates sit at consequential boundaries** — do not create approval fatigue for routine provisional context.
17. **Independence is structural** — the proposer must not control its own validator or authoriser.
18. **The model governs itself** — changes to Governance rules follow the same propose/validate/authorise discipline.
19. **Residual risk stays visible** — mitigations are not guarantees.

## Core files

- [`sanitised-memory.md`](sanitised-memory.md) — memory-governance core
- [`principles-worth-persisting.md`](principles-worth-persisting.md) — useful non-core principles that survived classification
- [`classification-examples.md`](classification-examples.md) — worked examples across all four classes
- [`memory-template.md`](memory-template.md) — blank review template
- [`enforcement-example.md`](enforcement-example.md) — prompt-level vs application-level enforcement example
- [`authority-boundaries.md`](authority-boundaries.md) — trust boundaries, evidence independence, roles, temporary renewal, recursive governance
- [`threat-model.md`](threat-model.md) — adversarial failure modes, mitigations, and residual risk

## Enforcement

Prompt text is not a security boundary.

For lightweight personal workflows, rules can live in persistent assistant context as behavioural guidance.

For consequential production systems, hard constraints should be enforced in application logic, permissions, middleware, identity/access controls, policy checks, storage lifecycle controls, or approval gates.

This repository defines policy and lifecycle semantics. It does not prove that a deployment enforces them.

## Use it

1. Export or review the persistent context your assistant is using.
2. Remove secrets and obviously sensitive material before sharing anything.
3. Assign each item a proposed `Class` and descriptive `Function`.
4. Validate sensitivity, provenance, ambiguity, authority, conflict, and scope.
5. Decide `Keep`, `Temporary`, or `Remove`.
6. If proposed as Governance, require explicit approval and identifiable supporting evidence.
7. If proposed as Preference, verify it does not alter authority or weaken controls.
8. Treat all non-Governance context as informative, not authoritative, when it is retrieved into active context.
9. If classification is ambiguous, default downward and attach a review condition.
10. For Temporary items, define expiry and renewal triggers.
11. During minimisation, preserve authority, provenance, scope, expiry, and safety qualifiers.
12. Do not inject persistent material into active context unless needed for the current task.
13. Put consequential rules behind real enforcement where consequences justify it.
14. Ensure storage lifecycle mechanics honour Temporary and Remove decisions as far as the underlying systems allow.
15. Review Governance conflicts explicitly rather than using recency as authority.
16. Review changes as diffs rather than silent replacements.
17. Apply the same Governance discipline to changes in this operating model itself.
18. Re-run review when a trigger fires, cumulative drift crosses a consequential boundary, or Temporary renewal reaches its forcing condition.

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
- a universal RBAC model
- a guarantee of perfect deletion across storage systems or providers
- a requirement to inject all persistent context into every prompt

It is a practical pattern:

**inspect → propose → validate → minimise → keep / temporary / remove → authorise → review**

## License

MIT License. See [`LICENSE`](LICENSE).
