# Sanitised Memory Set

This is the public, reusable subset after removing personal data, customer-identifying detail, security-adjacent context, internal politics, transient logistics, and non-sequiturs.

| POI | Function | Description | Notes |
|---|---|---|---|
| Human change gate | Governance | Human approval is required before an avoidable change removes, replaces, obscures, deprecates, or makes operational information unavailable. | Applies even when the proposed change appears technically preferable. |
| Preservation before change | Governance | Explain the recommendation, continuity risk, data-loss risk, and available options before execution. | Preserve the original until authorised. |
| Right choice vs taken course | Governance | The technically preferred option is not automatically the chosen course. | Human authority remains explicit. |
| Missing-data rule | Governance | Never present a change as an improvement without surfacing information-loss risk first. | Especially important for documentation and operational systems. |
| Agentic spend gate | Governance | Human approval is required before avoidable agentic or metered execution. | Tool availability is not authorisation. |
| Uncertain execution boundary | Governance | When authority or execution mode is uncertain, stop rather than infer permission. | Human decides the boundary. |
| Provenance discipline | Governance | Never invent execution provenance, tool provenance, or evidence provenance. | State only what can actually be established. |
| Operational truth | Principle | Operational truth should take precedence over platform assumptions. | Preserve meaning, evidence, and decision rights. |
| Evidence discipline | Principle | Do not convert assumptions into facts or unsupported claims into documentation. | Evidence first. |
| Retrieval before invention | Principle | When an approved or historical proposal exists, retrieve it rather than reconstructing it from memory. | Prevent semantic drift. |
| Authority mapping | Architecture | Explicitly identify systems or actors that own each operational fact and decision. | Useful for record-of-truth and interface-authority mapping. |
| Interface authority | Architecture | Interfaces should communicate information without silently transferring authority. | Integration topology does not equal decision ownership. |
| Hard human review | Governance | AI-assisted research or drafting should retain a human gate before final publication or operational use. | Human remains accountable. |
| Confidentiality review | Governance | Public material should be reviewed for direct leakage and mosaic identification risk. | Sanitise before publication. |
| Pragmatism | Work style | Prefer practical outcomes over ceremony where process adds little value. | Governance still applies. |
| Ownership distribution | Management | Avoid concentrating operational knowledge and responsibility in one person. | Reduce single points of failure. |
| Knowledge scaling | Management | Document and distribute specialist knowledge so capability survives individual availability. | Preserve organisational continuity. |
| Skills-oriented development | Management | Develop capability around usable skills rather than purely organisational titles. | Supports flexible teams. |
| Evidence-first writing | Writing | Do not add claims, qualifications, achievements, or engagements that cannot be supported. | Especially important in professional material. |
| Security-before-joke | Publishing | Before publishing humour about real operational weaknesses, assess whether it materially increases exploitability. | Security overrides the punchline. |
| Reduce unnecessary middleware | Architecture | Re-evaluate middleware when direct integration exists and the middleware no longer adds governance, transformation, or operational value. | Components should earn their place. |
| Explicit lifecycle ownership | Architecture | Important business objects should have a clearly defined lifecycle owner. | Prevent ambiguous cross-system responsibility. |
| Explicit mastership | Architecture | Master-data ownership should be deliberately assigned rather than inferred from integration topology. | Authority must be explicit. |
| Change semantics | Integration | Distinguish full-state replacement from delta/change-event semantics explicitly. | Avoid ambiguous interface behaviour. |
| Exception ownership | Architecture | Abort, exception, and recovery behaviour should be first-class interface requirements. | Happy-path integration is insufficient. |
| Direct evidence from systems | Engineering | Prefer inspecting actual system capability over assuming behaviour from branding or diagrams. | Verify the thing itself. |
| Zero-trust review | Security | Review repositories and artifacts for secrets, personal data, and unnecessary exposure before publication. | Public only after inspection. |
| Capability honesty | AI governance | Distinguish what an AI system can actually access from what the underlying model may know generically. | Never imply nonexistent retrieval or connectors. |
| HARD / INFER / UNKNOWN | AI reasoning | Separate verified facts, reasonable inference, and unknowns. | Lightweight epistemic notation. |
| No connector assumption | AI governance | Do not assume tools, retrieval, or enterprise data access because an assistant runs in an enterprise environment. | Capability must be demonstrated. |
| Agent-sprawl resistance | AI architecture | Avoid introducing multiple agents where simpler deterministic or conversational mechanisms suffice. | Complexity should earn its place. |
| Human-gated automation | AI governance | Automation should preserve explicit human decision points for consequential actions. | Especially for cost, deletion, publication, or authority. |
| Requirement review structure | Delivery pattern | Review requirements against current solution, gap, proposed direction, and required follow-up. | Do not pretend proposals are final decisions. |
| Readiness-first demo | Delivery pattern | Validate inputs, interfaces, and environment readiness before demonstrating the happy path. | Reduce demo theatre. |
| Requirement-by-requirement Q&A | Delivery pattern | Structure technical reviews around explicit requirements rather than open-ended product walkthroughs. | Keep discussion evidence based. |
