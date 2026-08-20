# Classification Examples

These examples show the classification process rather than only the final table.

## Example 1: Keep a Governance rule

**Raw memory**

> Never remove or overwrite operational information without asking first.

**Assessment**

- Stable across projects
- Directly changes assistant behaviour
- Low privacy risk once generalised
- High consequence if ignored
- Governance authority must not be self-assigned

**Proposed class**

Governance

**Function**

Governance

**Lifecycle**

Keep, subject to explicit approval and review-on-change

**Evidence / authorisation**

The model may explain why the rule is useful, but that explanation is not independent evidence for authority. Promotion requires explicit authorised judgement or identifiable supporting policy/evidence.

**Public form**

> Explain continuity and data-loss risk before destructive change, preserve the original, and require explicit approval before execution.

---

## Example 2: Distil private Operating Context

**Raw memory**

> Customer X uses middleware Y, direct connectivity was later available, and a demo failed on date Z because of that path.

**Assessment**

- Useful during an active project
- Customer-identifying
- Time-bound
- Contains a reusable architectural lesson
- Raw form should not persist publicly

**Proposed class**

Operating Context

**Function**

Architecture

**Lifecycle**

Temporary internally; Remove from public memory in raw form

**Review trigger**

Project close or architecture change.

**Public form**

> Re-evaluate middleware when direct integration exists and the middleware no longer adds governance, transformation, or operational value.

The private event is discarded. The reusable lesson survives.

---

## Example 3: Remove Ephemera

**Raw memory**

> A one-off cooking substitution discussed in a previous conversation.

**Assessment**

- No material effect on future AI behaviour
- Not stable
- Not operationally useful
- Persistence creates noise

**Proposed class**

Ephemera

**Function**

Miscellaneous

**Lifecycle**

Remove

**Active-context need**

None after the conversation where it was useful.

**Public form**

None.

The correct output of classification is sometimes deletion.

---

## Example 4: Keep a stable Preference

**Raw memory**

> Avoid a specific punctuation style in authored material.

**Assessment**

- Stable preference
- Low sensitivity
- Materially improves generated writing
- Easy to override when needed
- Does not weaken any authority, security, privacy, provenance, or confirmation control

**Proposed class**

Preference

**Function**

Writing

**Lifecycle**

Keep

**Authority boundary**

Non-authoritative. If the wording changed to something like “skip confirmation checks because I prefer fewer prompts,” it would stop being a Preference and become a Governance proposal.

**Active-context need**

Retrieve only when generating relevant authored material.

---

## Example 5: Ambiguity defaults downward

**Raw memory**

> Let's use PostgreSQL for this sprint.

**Assessment**

This could be misread as a stable technical Preference, current Operating Context, or durable architecture principle. The wording only establishes a sprint-scoped decision.

**Proposed class**

Operating Context

**Function**

Architecture / Delivery

**Lifecycle**

Temporary

**Review trigger**

Sprint end or architecture decision change.

When the evidence is ambiguous, choose the less persistent / less authoritative class and promote later only if new evidence justifies it.

---

## Example 6: Temporary renewal does not become permanent by neglect

**Raw memory**

> Keep the sprint architecture note for another sprint; we still need it.

**Assessment**

A single renewal may be justified. Repeating this indefinitely would create de facto permanent retention without a fresh Keep decision.

**Proposed class**

Operating Context

**Function**

Architecture / Delivery

**Lifecycle**

Temporary renewal

**Forcing condition**

The implementation defines a renewal threshold such as cumulative duration, renewal count, material scope change, or repeated use after the original purpose ends. Once triggered, the item must receive a fresh lifecycle review rather than inherit prior approval.

---

## Example 7: Model reasoning is not independent evidence

**Proposal**

> Promote this new rule into Governance because it improves safety.

**Model-generated justification**

> The rule is clearly necessary and should be permanent.

**Assessment**

The justification explains the proposal but proves nothing independently.

**Required evidence for consequential promotion**

One or more of:

- authoritative policy/source material
- system or audit evidence
- authenticated user decision
- independently generated application signal
- explicit human judgement

The proposer cannot bootstrap its own authority by writing a persuasive explanation.

---

## Example 8: The model governs changes to itself

**Proposal**

> Change the Governance rule so policy-control approval is no longer required for publication.

**Assessment**

This changes the authority model itself. A simple repository edit or model-generated diff is not sufficient authorisation.

**Process**

`PROPOSE → VALIDATE → AUTHORISE → VERSION → REVIEW`

The component proposing the change must not be able to unilaterally rewrite the mechanism that validates or authorises that same change.
