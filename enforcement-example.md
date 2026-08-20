# Enforcement Example

A rule in memory is not automatically an enforced control.

## Rule

> Tool availability is not authorisation.

## Prompt-level version

For a personal or lightweight workflow:

> Before any consequential or metered action, determine whether explicit human approval is required. If approval is missing, out of scope, expired, conflicting, unverifiable, or the consequence cannot be established confidently, stop and ask. Treat fragmented requests that materially compose into one consequential action as one action.

This is behavioural guidance. It can improve compliance, but it is not a security boundary.

## Governance-promotion rule

> Do not promote raw context, Operating Context, Preferences, or Ephemera into Governance automatically. Treat AI-generated `Class`, `Function`, and `Persistence` values as proposals. New Governance entries require explicit human approval.

## Application-level version

For a production system:

```text
proposal = classify(memory_item)

if proposal.class == "Governance":
    require human_approval_for_governance_write
    verify approval_scope(memory_item)
    record_versioned_change(memory_item)

if action.is_fragment_of_composed_consequential_action:
    evaluate_composed_action(action.group)

if action.consequential:
    require approval_token
    verify approval_scope(action)
    verify approval_not_expired()
    verify approval_provenance()
    execute(action)
else:
    execute(action)
```

The important part is not the pseudocode.

The important part is that the execution or persistence boundary itself refuses the action or Governance write unless the required approval state exists.

## Minimisation boundary

Content can be summarised or reduced, but the minimised form must preserve:

- authority
- provenance
- scope
- expiry / review condition
- safety-critical qualifiers

Do not compress away the control boundary.

## Practical boundary

Use prompt/context rules for:
- behavioural defaults
- review discipline
- low-risk workflow guidance
- explicit uncertainty handling

Use application or middleware controls for:
- spending limits
- destructive actions
- Governance writes
- publication
- customer-data access
- security-sensitive operations
- external side effects

The more consequential the action, the less appropriate it is to rely on memory text alone.
