# Memory Review Template

| POI | Raw memory / context | Proposed Class | Function | Persistence | Provisional? | Expiry / review trigger | Human approval required? | Control metadata preserved? | Active-context need? | Storage cleanup scope | Public form | Why |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|  |  | Governance / Operating Context / Preference / Ephemera |  | Keep / Temporary / Remove | Yes / No |  | Yes / No | Authority / provenance / scope / expiry / safety qualifiers | Always / Conditional / No | Index / embedding / cache / replica / derived store / N/A |  |  |

## Review questions

- Does this help the assistant make materially better decisions?
- Is it still true?
- Is it stable enough to persist?
- Is it appropriate to persist?
- Is the proposed class Governance, Operating Context, Preference, or Ephemera?
- What function does it serve?
- Should it be Keep, Temporary, or Remove?
- Can this remain provisional instead of receiving immediate authority?
- If classification is ambiguous, have you chosen the less persistent / less authoritative class?
- If Temporary, what is the expiry or review trigger?
- If Governance, what is the explicit review trigger or `review-on-change` condition?
- If proposed as Governance, has a human explicitly approved that promotion?
- Could this item be adversarially phrased to masquerade as Governance or Preference?
- Is approval missing, out of scope, expired, conflicting, or unverifiable?
- If several small requests compose into one consequential action, have they been reviewed as one action?
- Would publication expose personal, confidential, security, or customer information?
- Can the same value be achieved with less retained information?
- During minimisation, are authority, provenance, scope, expiry, and safety-critical qualifiers preserved?
- Can private context be distilled into a reusable principle without retaining the identifying event?
- Is the classification independently validated where consequences are high?
- Does this item need to be injected into active context now, or can it remain stored until relevant?
- If `Temporary` or `Remove`, which indexes, embeddings, caches, replicas, or derived stores must honour that lifecycle decision?
- Does this require a real enforcement mechanism outside prompt text?
- Will the change be visible in an auditable diff rather than silently replacing prior governance?
