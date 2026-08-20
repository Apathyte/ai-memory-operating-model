# Threat Model

This project is a documentation and decision pattern, not a security product. Its main attack surface is **bad persistence and authority decisions**: retaining the wrong thing, granting it too much authority, collapsing supposedly independent gates, losing control metadata during minimisation, or failing to propagate lifecycle decisions to real storage systems.

A named control below is a mitigation, not proof that an implementation enforces it.

## 1. Classification hijacking

**Risk:** adversarial or misleading text is framed as a harmless Preference, Operating Context, or Governance rule.

**Mitigation:** AI classification is provisional; Governance promotion is write-protected; ambiguity defaults downward; consequential classifications require validation.

**Residual risk:** a weak or compromised validator can still accept a bad proposal.

## 2. Governance poisoning

**Risk:** a malicious or mistaken item enters Governance and inherits long-lived authority.

**Mitigation:** Governance cannot self-assign; new entries require explicit authorisation; changes are reviewable, revocable, versioned, and diffable.

**Residual risk:** the authorisation mechanism itself may be compromised or misconfigured.

## 3. Validator/authoriser collapse

**Risk:** the same AI-controlled authority channel proposes, validates, and authorises a consequential change.

**Mitigation:** independence must be structural. The proposer must not be able to unilaterally alter the validator, policy, approval state, credentials, or authorisation mechanism that grants the change authority.

**Residual risk:** actual separation depends on deployment architecture, identity, credentials, and change control outside this repo.

## 4. Preference privilege escalation

**Risk:** an authority or safety change is reframed as a harmless Preference, for example: "I prefer outputs that skip confirmation checks."

**Mitigation:** Preferences are non-authoritative. If a Preference would weaken confirmation, security, privacy, provenance, or Governance controls, it becomes a Governance proposal.

**Residual risk:** subtle behavioural changes can be hard to recognise as authority changes.

## 5. Approval laundering, salami attacks, cumulative drift, and human fatigue

**Risk:** one consequential change is split into many harmless-looking micro-changes, or high proposal volume turns review into rubber-stamping.

**Mitigation:** materially composing requests are evaluated together; repeated low-risk changes that alter authority, safety, confirmation behaviour, or scope trigger consequential review; low-risk context may stay provisional.

**Residual risk:** cumulative tracking and trigger thresholds are implementation-specific and can be incomplete across long time horizons.

## 6. Temporary-renewal laundering

**Risk:** Temporary context is repeatedly renewed until it becomes de facto permanent without ever receiving a fresh Keep decision.

**Mitigation:** implementations define a forcing function such as cumulative duration, renewal count, scope change, or repeated use after the original purpose ends. When triggered, renewal becomes a fresh lifecycle decision.

**Residual risk:** weak renewal policies can still permit indefinite retention by neglect.

## 7. Lossy minimisation

**Risk:** summarisation removes the authority, provenance, scope, expiry, or safety qualifier that made the original context safe.

**Mitigation:** minimise content, not control metadata.

**Residual risk:** deciding which qualifiers are safety-critical still requires judgement.

## 8. Metadata trust and metadata exhaustion

**Risk:** an application trusts AI-generated `Class`, `Function`, or `Lifecycle` metadata, or accumulated audit metadata bloats active context.

**Mitigation:** treat AI metadata as proposals; validate consequential decisions outside the proposing model; keep lifecycle metadata outside active prompt context where possible; retrieve narrowly; apply retention discipline to metadata too.

**Residual risk:** implementation mistakes can still over-trust stored metadata or over-inject it.

## 9. False certainty

**Risk:** an agent acts despite ambiguous authority.

**Stop conditions:** approval missing, out of scope, expired, conflicting, unverifiable, or consequences unclear.

**Residual risk:** the agent may fail to detect that a stop condition exists.

## 10. Governance conflict and multi-actor disagreement

**Risk:** two individually valid Governance rules or authorisers conflict across humans, sessions, or policy changes.

**Mitigation:** no last-write-wins; explicitly scoped approved rules may override general rules within scope; newer rules only supersede when the change itself was authorised; unresolved precedence stops and escalates.

**Residual risk:** local role and RBAC models remain implementation-specific.

## 11. Self-referential evidence

**Risk:** the AI proposes a consequential change and then cites its own generated justification as the evidence that the change should be authorised.

**Mitigation:** model-generated reasoning may explain a proposal but is not independent evidence for authority. Prefer identifiable source material, logs, approved policy, authenticated decisions, independent application signals, or explicit human judgement.

**Residual risk:** source material can itself be wrong, poisoned, stale, or misleading.

## 12. False retrieval or provenance

**Risk:** an assistant claims to have retrieved or verified material when it reconstructed it from memory or model knowledge.

**Mitigation:** a retrieval claim is not evidence unless the source can be identified or surfaced.

**Residual risk:** source identification does not itself prove source quality.

## 13. Stale Governance

**Risk:** a once-valid rule remains active after policy, authority, environment, or system assumptions change.

**Mitigation:** `Keep` does not mean permanent; Governance has explicit review triggers or `review-on-change` conditions.

**Residual risk:** a relevant change may occur without firing the chosen trigger.

## 14. Privacy and mosaic leakage

**Risk:** individually harmless facts combine into identifying customer, organisational, personal, or infrastructure detail.

**Mitigation:** do not publish raw memory dumps; prefer distilled principles; review for mosaic risk, not only direct identifiers.

**Residual risk:** mosaic identification is contextual and cannot be reduced to a perfect checklist.

## 15. Context-window tax

**Risk:** policy, provenance, expiry, approval, and lifecycle metadata is repeatedly injected into active prompts, increasing latency/cost and reducing reasoning space.

**Mitigation:** persistence does not imply prompt injection; store broadly only when justified and retrieve the minimum required for the current decision.

**Residual risk:** some decisions genuinely require substantial control context.

## 16. Storage-policy disconnect and incomplete deletion

**Risk:** the policy says Temporary or Remove while embeddings, indexes, caches, replicas, derived stores, logs, backups, or provider-held copies remain retrievable or retained.

**Mitigation:** lifecycle semantics propagate to every applicable persistence layer under the system's control; external retention and storage limits are documented; perfect erasure is not claimed where the stack cannot guarantee it.

**Residual risk:** data outside the system's control may remain retained according to external capabilities and policies.

## 17. Taxonomy ambiguity

**Risk:** real context sits between classes and the classifier chooses a more persistent or more authoritative interpretation.

**Mitigation:** choose the less persistent / less authoritative class, attach a review condition, and promote later only with sufficient evidence and authority.

**Residual risk:** ambiguity cannot be eliminated; the default only makes the error safer.

## 18. Recursive governance / control-plane compromise

**Risk:** a compromised deployment or maintainer edits the Governance rules, validator, or authorisation mechanism itself instead of attacking governed memory directly.

**Mitigation:** changes to Governance rules follow **PROPOSE → VALIDATE → AUTHORISE → VERSION → REVIEW**. The proposer must not be able to unilaterally modify the mechanism that validates or authorises that same change.

**Residual risk:** this repo cannot secure the deployment pipeline, credentials, repository permissions, or policy engine that implements that boundary.

## Authorisation boundary

This model is **human-governed**, not necessarily human-in-the-loop for every action.

Consequential transitions require either explicit human approval or an application/policy control whose authority and independence were deliberately established.

An automated policy gate is independent only if the proposing model cannot unilaterally alter the policy, approval state, credentials, or authority path that grants the decision.

## Security boundary

Prompt-level rules can guide behaviour. They do not create a hard security boundary.

Where consequences justify it, enforce policy in application logic, identity/access controls, permissions, middleware, approval gates, storage lifecycle controls, deployment/change controls, or other mechanisms outside the model's persistent context.

The framework defines semantics. The implementation carries the guarantee.
