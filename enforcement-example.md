# Enforcement Example

A rule in memory is not automatically an enforced control.

## Rule

> Tool availability is not authorisation.

## Prompt-level version

For a personal or lightweight workflow:

> Before any consequential or metered action, determine whether explicit authority exists. If approval is missing, out of scope, expired, conflicting, unverifiable, or the consequence cannot be established confidently, stop and ask. Treat fragmented requests that materially compose into one consequential action as one action.

This is behavioural guidance. It can improve compliance, but it is not a security boundary.

## Provisional fast path

Low-risk context may be classified provisionally without stopping the workflow for immediate approval.

Provisional context must not silently gain higher authority merely because it has been stored, repeatedly retrieved, or repeatedly renewed.

Require a stronger gate when crossing into Governance, consequential use, publication, destructive or metered action, sensitive-data access, material policy change, or another high-impact boundary.

## Governance-promotion rule

> Do not promote raw context, Operating Context, Preferences, or Ephemera into Governance automatically. Treat AI-generated `Class`, `Function`, and `Lifecycle` values as proposals. New Governance entries require explicit authorisation.

## Trust-boundary rule

An automated validator or policy gate is not independent merely because it is a separate component.

For consequential transitions, the proposing model must not be able to unilaterally alter:

- validation criteria
- policy configuration
- approval state
- authorisation credentials
- deployment/change path of the authoriser

The implementation may use separate credentials, permissions, deployment paths, policy engines, or other controls. The invariant is that the proposer cannot control the thing that grants it authority.

## Evidence rule

Model-generated reasoning can explain a proposal, but it is not independent evidence for granting authority.

For consequential promotion, require identifiable supporting evidence such as authoritative source material, logs, approved policy records, authenticated decisions, independent application signals, or explicit human judgement.

## Application-level sketch

```text
proposal = classify(memory_item)

if proposal.is_ambiguous:
    proposal = downgrade_lifecycle_and_authority(proposal)
    attach_review_trigger(proposal)

store_as_provisional(proposal)

if proposal.class == "Governance":
    require_authorisation_from_independent_boundary()
    verify_authoriser_scope(memory_item)
    verify_authoriser_cannot_be_modified_by_proposer()
    require_independent_evidence_or_human_judgement()
    record_versioned_change(memory_item)

if memory_item.lifecycle == "Temporary":
    increment_renewal_state(memory_item)
    if renewal_forcing_condition_reached(memory_item):
        require_fresh_lifecycle_decision(memory_item)

if action.is_fragment_of_composed_consequential_action:
    evaluate_composed_action(action.group)

if cumulative_changes_alter_authority_or_safety(action.subject):
    require_consequential_review(action.subject)

if action.consequential:
    require_approval_token()
    verify_approval_scope(action)
    verify_approval_not_expired()
    verify_approval_provenance()
    execute(action)
else:
    execute(action)
```

The important part is not the pseudocode.

The important part is that the persistence or execution boundary refuses consequential authority unless the required approval, evidence, scope, and trust-boundary conditions exist.

## Recursive governance

Changes to the Governance rules themselves should use the same discipline:

```text
propose(governance_change)
validate(governance_change)
authorise_from_independent_boundary(governance_change)
version(governance_change)
review_on_trigger(governance_change)
```

A proposer must not be able to rewrite its own authoriser and call that approval.

## Minimisation boundary

Content can be summarised or reduced, but the minimised form must preserve authority, provenance, scope, expiry/review state, and safety-critical qualifiers.

Do not compress away the control boundary.

## Prompt-context boundary

Persistence does not mean every stored item should be injected into every prompt.

Retrieve only the context needed for the current decision. Keep lifecycle, provenance, approval, and other policy metadata outside active prompt context where possible unless the model needs that metadata to reason safely about the current action.

## Storage lifecycle boundary

A lifecycle decision must be reflected in the systems that can still retrieve the item.

```text
if memory.lifecycle == "Temporary":
    apply_expiry_and_renewal_rules(memory)

if memory.lifecycle == "Remove":
    remove_from_primary_store(memory)
    remove_or_invalidate_applicable_embeddings(memory)
    remove_or_invalidate_applicable_indexes(memory)
    remove_or_invalidate_applicable_caches(memory)
    handle_derived_stores_and_replicas(memory)
```

External logs, backups, provider retention, or storage limits may prevent perfect erasure. Document those limits rather than overstating the guarantee.

## Practical boundary

Use prompt/context rules for behavioural defaults, review discipline, low-risk provisional classification, and explicit uncertainty handling.

Use application, identity/access, storage, deployment, or middleware controls for consequential execution, Governance writes, independent authorisation, sensitive-data access, expiry/deletion mechanics, and changes to the Governance control plane itself.

The more consequential the action, the less appropriate it is to rely on memory text alone.
