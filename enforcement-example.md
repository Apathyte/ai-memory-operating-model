# Enforcement Example

A rule in memory is not automatically an enforced control.

## Rule

> Tool availability is not authorisation.

## Prompt-level version

For a personal or lightweight workflow:

> Before any consequential or metered action, determine whether explicit human approval is required. If approval is missing, out of scope, expired, conflicting, unverifiable, or the consequence cannot be established confidently, stop and ask. Treat fragmented requests that materially compose into one consequential action as one action.

This is behavioural guidance. It can improve compliance, but it is not a security boundary.

## Provisional fast path

Low-risk context may be classified provisionally without stopping the workflow for immediate approval.

Provisional context must not silently gain higher authority merely because it has been stored or repeatedly retrieved.

Require a stronger gate when crossing into:

- Governance
- consequential use
- publication
- destructive or metered action
- sensitive-data access
- other high-impact boundaries

## Governance-promotion rule

> Do not promote raw context, Operating Context, Preferences, or Ephemera into Governance automatically. Treat AI-generated `Class`, `Function`, and `Persistence` values as proposals. New Governance entries require explicit human approval.

## Application-level version

For a production system:

```text
proposal = classify(memory_item)

if proposal.is_ambiguous:
    proposal = downgrade_persistence_and_authority(proposal)
    attach_review_trigger(proposal)

store_as_provisional(proposal)

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

The important part is that the execution or persistence boundary itself refuses the consequential action or Governance write unless the required approval state exists.

## Minimisation boundary

Content can be summarised or reduced, but the minimised form must preserve:

- authority
- provenance
- scope
- expiry / review condition
- safety-critical qualifiers

Do not compress away the control boundary.

## Prompt-context boundary

Persistence does not mean every stored item should be injected into every prompt.

Retrieve only the context needed for the current decision. Keep lifecycle, provenance, approval, and other policy metadata outside the active prompt where possible unless the model needs that metadata to reason safely about the current action.

## Storage lifecycle boundary

A policy decision must be reflected in the systems that can still retrieve the item.

For real memory infrastructure:

```text
if memory.persistence == "Temporary":
    apply_expiry_or_review_trigger(memory)

if memory.persistence == "Remove":
    remove_from_primary_store(memory)
    remove_or_invalidate_applicable_embeddings(memory)
    remove_or_invalidate_applicable_indexes(memory)
    remove_or_invalidate_applicable_caches(memory)
    handle_derived_stores_and_replicas(memory)
```

The exact implementation will vary. The principle is that a `Remove` label in documentation is not enough if the item remains retrievable elsewhere.

## Practical boundary

Use prompt/context rules for:

- behavioural defaults
- review discipline
- low-risk provisional classification
- explicit uncertainty handling

Use application, storage, or middleware controls for:

- spending limits
- destructive actions
- Governance writes
- publication
- customer-data access
- security-sensitive operations
- external side effects
- expiry and deletion mechanics

The more consequential the action, the less appropriate it is to rely on memory text alone.
