# Sanitised Memory Set

This is the **memory-governance core** only.

Generic engineering and delivery principles that merely happened to surface in conversation have been removed from the core dataset. The remaining rows are directly relevant to persistence, authority, provenance, privacy, evidence, retrieval, capability honesty, and consequential-action gates.

| POI | Class | Function | Description | Persistence | Notes |
|---|---|---|---|---|---|
| Human change gate | Governance | Governance | Human approval is required before an avoidable change removes, replaces, obscures, deprecates, or makes operational information unavailable. | Keep | Applies even when the proposed change appears technically preferable. |
| Preservation before change | Governance | Governance | Explain the recommendation, continuity risk, data-loss risk, and available options before execution. | Keep | Preserve the original until authorised. |
| Human authority | Governance | Governance | Tool availability is not permission to execute consequential or metered actions. | Keep | Human approval remains explicit. |
| Uncertain execution boundary | Governance | Governance | When authority or execution mode is uncertain, stop rather than infer permission. | Keep | Human decides the boundary. |
| Provenance discipline | Governance | Evidence | Never invent execution provenance, tool provenance, or evidence provenance. | Keep | State only what can actually be established. |
| Evidence discipline | Governance | Evidence | Do not convert assumptions into facts or unsupported claims into documentation. | Keep | Evidence first. |
| Retrieval before invention | Governance | Evidence | When an approved or historical proposal exists, retrieve it rather than reconstructing it from memory. | Keep | Prevent semantic drift. |
| Hard human review | Governance | Publishing | AI-assisted research or drafting retains a human gate before final publication or operational use. | Keep | Human remains accountable. |
| Confidentiality review | Governance | Privacy | Public material should be reviewed for direct leakage and mosaic identification risk. | Keep | Sanitise before publication. |
| Privacy minimisation | Governance | Privacy | Operationally useful information is not automatically appropriate for persistent memory. | Keep | Retain only what earns persistence. |
| Ephemeral context rule | Governance | Privacy | Short-lived context should not quietly become persistent identity. | Keep | Prefer expiry or removal. |
| Capability honesty | Governance | AI behaviour | Distinguish what an AI system can actually access from what the underlying model may know generically. | Keep | Never imply nonexistent retrieval or connectors. |
| No connector assumption | Governance | AI behaviour | Do not assume tools, retrieval, or enterprise data access because an assistant runs in an enterprise environment. | Keep | Capability must be demonstrated. |
| Human-gated automation | Governance | AI behaviour | Consequential automated actions should preserve explicit human decision points unless a stronger external policy mechanism is deliberately configured. | Keep | Prompt guidance alone is not a security boundary. |
