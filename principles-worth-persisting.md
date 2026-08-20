# Principles Worth Persisting

The core memory-governance controls live in [`sanitised-memory.md`](sanitised-memory.md).

This file serves a different purpose.

These are **sanitised examples of principles that survived the classification exercise because they materially improve future work**, even though they are not themselves all controls about memory governance.

That distinction matters:

- `sanitised-memory.md` answers: **what governs persistence, authority, evidence, privacy, and consequential action?**
- this file answers: **what kinds of non-sensitive principles may actually be worth persisting once the model has decided they earn a place?**

The classifications below are illustrative, not universal. A different user may classify the same idea differently depending on how they want the assistant to use it.

| POI | Class | Function | Description | Persistence | Why it earns a place |
|---|---|---|---|---|---|
| HARD / INFER / UNKNOWN | Governance | AI reasoning | Separate verified facts, reasonable inference, and unknowns explicitly. | Keep | Improves epistemic discipline and makes uncertainty visible instead of laundering inference into fact. |
| Operational truth | Preference | Principle | Prefer operational reality over platform assumptions when the two diverge. | Keep | Anchors advice to what is actually happening rather than what a product or process supposedly guarantees. |
| Authority mapping | Preference | Architecture | Explicitly identify the system or actor that owns each operational fact and decision. | Keep | Prevents ambiguous ownership and hidden authority transfer. |
| Interface authority | Preference | Architecture | Treat interfaces as information exchange, not automatic transfer of decision authority. | Keep | Keeps integration topology separate from business ownership. |
| Evidence-first writing | Governance | Writing | Do not add claims, achievements, qualifications, or conclusions that cannot be supported. | Keep | Reduces fabrication and keeps authored material defensible. |
| Security-before-joke | Governance | Publishing | Before publishing humour about a real weakness, assess whether the joke materially increases exploitability. | Keep | Preserves voice without trading away security for the punchline. |
| Agent-sprawl resistance | Preference | AI architecture | Avoid introducing multiple agents where simpler conversational or deterministic mechanisms are sufficient. | Keep | Prevents unnecessary complexity and cost. |
| Direct evidence from systems | Preference | Engineering | Prefer inspecting actual system capability over assuming behaviour from branding, diagrams, or product claims. | Keep | Replaces assumption with verification. |
| Reduce unnecessary middleware | Preference | Architecture | Re-evaluate middleware when direct integration exists and the middleware no longer adds governance, transformation, or operational value. | Keep | Keeps legacy components from surviving purely through inertia. |
| Explicit lifecycle ownership | Preference | Architecture | Important business objects should have a clearly defined lifecycle owner. | Keep | Prevents ambiguous cross-system responsibility. |
| Explicit mastership | Preference | Architecture | Master-data ownership should be deliberately assigned rather than inferred from integration topology. | Keep | Makes authority explicit. |
| Change semantics | Preference | Integration | Distinguish full-state replacement from delta/change-event semantics explicitly. | Keep | Avoids ambiguous interface behaviour. |
| Exception ownership | Preference | Architecture | Abort, exception, and recovery behaviour should be first-class interface requirements. | Keep | Prevents happy-path-only designs. |
| Pragmatism | Preference | Work style | Prefer practical outcomes over ceremony where process adds little value. | Keep | Gives future advice a stable operating bias without pretending process is irrelevant. |
| Ownership distribution | Preference | Management | Avoid concentrating operational knowledge and responsibility in one person. | Keep | Reduces single points of failure. |
| Knowledge scaling | Preference | Management | Document and distribute specialist knowledge so capability survives individual availability. | Keep | Preserves organisational continuity. |
| Skills-oriented development | Preference | Management | Develop capability around usable skills rather than purely organisational titles. | Keep | Supports flexible teams and clearer capability planning. |
| Readiness-first demo | Preference | Delivery | Validate inputs, interfaces, and environment readiness before demonstrating the happy path. | Keep | Reduces demo theatre and avoidable failure. |
| Requirement-by-requirement Q&A | Preference | Delivery | Structure technical reviews around explicit requirements rather than open-ended product walkthroughs. | Keep | Keeps discussions evidence-based and decision-oriented. |

## Why keep this file separate?

Because otherwise two different questions get mixed together:

1. **How should persistent context be governed?**
2. **Which useful principles happened to survive that governance process?**

The first question defines the operating model.

The second provides examples of the kind of value the model can preserve.

Keeping them separate lets the taxonomy stay clean **without throwing away good memory just because it is not itself a memory-governance rule**.
