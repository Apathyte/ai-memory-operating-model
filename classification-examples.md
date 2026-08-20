# Classification Examples

These examples show the classification process rather than only the final table.

## Example 1: Keep the governance rule

**Raw memory**

> Never remove or overwrite operational information without asking first.

**Assessment**

- Stable across projects
- Directly changes assistant behaviour
- Low privacy risk once generalized
- High consequence if ignored

**Class**

Governance

**Function**

Governance

**Persistence**

Keep

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

**Class**

Operating Context

**Function**

Architecture

**Persistence**

Temporary internally; Remove from public memory in raw form

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

**Class**

Ephemera

**Function**

Miscellaneous

**Persistence**

Remove

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

**Class**

Preference

**Function**

Writing

**Persistence**

Keep

**Public form**

A generic style preference is safe to retain if it consistently improves output.
