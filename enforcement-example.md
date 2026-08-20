# Enforcement Example

A rule in memory is not automatically an enforced control.

## Rule

> Tool availability is not authorisation.

## Prompt-level version

For a personal or lightweight workflow:

> Before any consequential or metered action, determine whether explicit human approval is required. If authority is uncertain, stop and ask.

This is behavioural guidance. It can improve compliance, but it is not a security boundary.

## Application-level version

For a production system:

```text
if action.consequential:
    require approval_token
    verify approval_scope(action)
    verify approval_not_expired()
    execute(action)
else:
    execute(action)
```

The important part is not the pseudocode.

The important part is that the execution endpoint itself refuses the action unless the required approval state exists.

## Practical boundary

Use prompt/context rules for:
- behavioural defaults
- review discipline
- low-risk workflow guidance
- explicit uncertainty handling

Use application or middleware controls for:
- spending limits
- destructive actions
- publication
- customer-data access
- security-sensitive operations
- external side effects

The more consequential the action, the less appropriate it is to rely on memory text alone.
