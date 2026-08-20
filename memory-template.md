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
- If proposed as Preference, could it weaken confirmation, security, privacy, provenance, or Governance controls? If yes, treat it as a Governance proposal instead.
- Could this item be adversarially phrased to masquerade as Governance or Preference?
- Is approval missing, out of scope, expired, conflicting, or unverifiable?
- If two valid Governance rules conflict, is one explicitly scoped over the other? If not, stop and escalate rather than using last-write-wins.
- If several small requests compose into one consequential action, have they been reviewed as one action?
- Have repeated low-risk changes cumulatively altered authority, safety, confirmation behaviour, or scope?
- Would publication expose personal, confidential, security, or customer information?
- Can the same value be achieved with less retained information?
- During minimisation, are authority, provenance, scope, expiry, and safety-critical qualifiers preserved?
- Can private context be distilled into a reusable principle without retaining the identifying event?
- Is the classification independently validated where consequences are high?
- Does this item need to be injected into active context now, or can it remain stored until relevant?
- Is control metadata itself bounded, expired, and retrieved only when needed?
- If `Temporary` or `Remove`, which stores under your control must honour that lifecycle decision?
- Are there external logs, backups, provider retention, or storage limitations that prevent a stronger deletion claim?
- Does this require a real enforcement mechanism outside prompt text?
- Is human review reserved for an authority transition or consequential boundary rather than routine low-risk writes?
- Will the change be visible in an auditable diff rather than silently replacing prior governance?
