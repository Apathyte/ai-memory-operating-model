# Sanitised Memory Set

This is the **memory-governance core** only.

Generic engineering and delivery principles live separately in [`principles-worth-persisting.md`](principles-worth-persisting.md). The rows below are directly relevant to lifecycle, authority, provenance, privacy, evidence, retrieval, trust boundaries, governance promotion, and consequential-action gates.

| POI | Class | Function | Description | Lifecycle | Review / enforcement note |
|---|---|---|---|---|---|
| Governance write protection | Governance | Governance | Raw context, Operating Context, Preferences, and Ephemera must not be promoted automatically into Governance. | Keep | New Governance entries require explicit approval. |
| Governance reviewability | Governance | Governance | Governance entries remain reviewable and revocable. | Keep | `Keep` does not mean permanent or beyond challenge. |
| Governance audit trail | Governance | Governance | Governance changes should be versioned and diffable rather than silently replaced. | Keep | A diff is evidence of change, not proof of proper authorisation. |
| Recursive governance | Governance | Governance | Changes to Governance rules must pass the same propose, validate, authorise, version, and review discipline as governed context. | Keep | The proposer must not unilaterally alter its own validator or authoriser. |
| Governance conflict resolution | Governance | Governance | Conflicting Governance entries must not silently resolve by last-write-wins. | Keep | Prefer explicit scoped authority over general authority; otherwise stop and escalate. |
| Preference non-authority | Governance | Governance | Preferences must not weaken confirmation, security, privacy, provenance, or Governance controls. | Keep | A preference that changes authority or safety is a Governance proposal. |
| Human change gate | Governance | Governance | Human approval is required before an avoidable change removes, replaces, obscures, deprecates, or makes operational information unavailable. | Keep | Applies even when the proposed change appears technically preferable. |
| Preservation before change | Governance | Governance | Explain the recommendation, continuity risk, data-loss risk, and available options before execution. | Keep | Preserve the original until authorised. |
| Human authority | Governance | Governance | Tool availability is not permission to execute consequential or metered actions. | Keep | Human approval remains explicit where policy requires it. |
| Trust-boundary independence | Governance | Governance | An automated validator or authoriser is independent only if the proposer cannot unilaterally change the policy, approval state, credentials, or authority path that grants the decision. | Keep | Independence is structural, not a label. |
| Approval composition | Governance | Governance | Multiple small requests that materially form one consequential action must be evaluated as one action. | Keep | Prevents approval laundering through fragmentation. |
| Cumulative drift review | Governance | Governance | Repeated low-risk changes that cumulatively alter authority, safety, confirmation behaviour, or scope must be promoted for consequential review. | Keep | Prevents salami-style escalation through gradual drift. |
| Temporary renewal boundary | Governance | Lifecycle | Temporary context must not renew itself indefinitely into de facto Keep status. | Keep | Define a forcing function such as duration, renewal count, scope change, or use beyond the original purpose. |
| Uncertain execution boundary | Governance | Governance | Stop rather than infer permission when approval is missing, out of scope, expired, conflicting, unverifiable, or consequences cannot be established confidently. | Keep | Authority must be established outside raw model self-assertion. |
| AI classification is provisional | Governance | Governance | AI-generated `Class`, `Function`, and `Lifecycle` values are proposals, not trusted policy metadata. | Keep | High-consequence classifications need independent validation. |
| Provenance discipline | Governance | Evidence | Never invent execution provenance, tool provenance, or evidence provenance. | Keep | A retrieval claim is not evidence unless the source can be identified or surfaced. |
| Independent evidence for authority | Governance | Evidence | Model-generated reasoning may explain a proposal but is not independent evidence for granting authority. | Keep | Prefer authoritative source material, logs, approved policy, authenticated decisions, independent signals, or explicit human judgement. |
| Evidence discipline | Governance | Evidence | Do not convert assumptions into facts or unsupported claims into documentation. | Keep | Evidence first. |
| Retrieval before invention | Governance | Evidence | When an approved or historical proposal exists, retrieve it rather than reconstructing it from memory. | Keep | Prevent semantic drift. |
| Minimisation preserves controls | Governance | Privacy | Minimisation may reduce content but must preserve authority, provenance, scope, expiry, and safety-critical qualifiers. | Keep | Do not compress away the control boundary. |
| Confidentiality review | Governance | Privacy | Public material should be reviewed for direct leakage and mosaic identification risk. | Keep | Sanitise before publication. |
| Privacy minimisation | Governance | Privacy | Operationally useful information is not automatically appropriate for persistent memory. | Keep | Retain only what earns persistence. |
| Ephemeral context rule | Governance | Privacy | Short-lived context should not quietly become persistent identity. | Keep | Prefer expiry or removal. |
| Capability honesty | Governance | AI behaviour | Distinguish what an AI system can actually access from what the underlying model may know generically. | Keep | Never imply nonexistent retrieval or connectors. |
| No connector assumption | Governance | AI behaviour | Do not assume tools, retrieval, or enterprise data access because an assistant runs in an enterprise environment. | Keep | Capability must be demonstrated. |
| Consequential authorisation | Governance | AI behaviour | Consequential transitions require explicit human approval or a structurally independent application/policy control. | Keep | Human-governed does not mean human-clicked at every action boundary. |
| Gate fatigue control | Governance | AI behaviour | Human review is reserved for authority transitions, consequential use, publication, sensitive access, or material policy change. | Keep | Low-risk proposals may remain provisional to avoid rubber-stamping. |
| Metadata minimisation | Governance | AI behaviour | Persisted control metadata should not be injected into active context unless needed, and metadata itself needs retention discipline. | Keep | Prevent context-window exhaustion and governance metadata bloat. |
