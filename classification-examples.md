# Classification Examples

These examples show the classification process rather than only the final table.

## Example 1: Keep the governance rule

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

**Persistence**

Keep, subject to human approval and review-on-change

**Authorisation**

Explicit human approval required before promotion into Governance.

**Public form**

> Explain continuity and data-loss risk before destructive change, preserve the original, and require explicit human approval before execution.

---

## Example 2: Distill private operating context

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

**Persistence**

Temporary internally; Remove from public memory in raw form

**Lifecycle**

Attach a project-close or architecture-change review trigger. A Remove decision must also cover any applicable derived store if this context is persisted outside the conversation layer.

**Public form**

> Re-evaluate middleware when direct integration exists and the middleware no longer adds governance, transformation, or operational value.

The private event is discarded. The reusable lesson survives.

---

## Example 3: Remove ephemera

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

**Persistence**

Remove

**Active-context need**

None after the conversation where it was useful.

**Public form**

None.

The correct output of classification is sometimes deletion.

---

## Example 4: Keep a stable preference

**Raw memory**

> Avoid a specific punctuation style in authored material.

**Assessment**

- Stable preference
- Low sensitivity
- Materially improves generated writing
- Easy to override when needed

**Proposed class**

Preference

**Function**

Writing

**Persistence**

Keep

**Active-context need**

Retrieve or inject only when generating relevant authored material; persistence does not require constant prompt presence.

**Public form**

A generic style preference is safe to retain if it consistently improves output.

---

## Example 5: Ambiguity defaults downward

**Raw memory**

> Let's use PostgreSQL for this sprint.

**Assessment**

This could be misread as:

- a stable technical Preference
- current Operating Context
- a durable architecture principle

The wording only establishes a sprint-scoped decision.

**Proposed class**

Operating Context

**Function**

Architecture / Delivery

**Persistence**

Temporary

**Review trigger**

Sprint end or architecture decision change.

**Why not Preference?**

There is not enough evidence that this is a stable human preference.

**Why not Governance?**

Nothing in the statement grants policy authority.

When the evidence is ambiguous, choose the less persistent / less authoritative class and promote later only if new evidence justifies it.
