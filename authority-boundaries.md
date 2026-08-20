# Authority and Trust Boundaries

This file defines the parts of the model that cannot be left as labels such as "independent", "approved", or "authorised" without saying what those words mean.

## 1. Independence is a property, not a label

An automated validator or policy control is independent only when the proposing model or workflow cannot unilaterally change the mechanism that validates or authorises its proposal.

For consequential transitions, independence should be established through a separate trust boundary appropriate to the implementation. Examples can include:

- separate credentials or permission scope
- a separately managed policy configuration
- a separate deployment/change path
- an approval state the proposing model cannot mint or alter
- an external rules engine or deterministic check outside the proposing model's authority

The exact mechanism is implementation-specific. The invariant is not:

> a different component exists

It is:

> the proposer cannot unilaterally control the thing that grants it authority.

## 2. Propose, Validate and Authorise must not collapse into self-approval

Automation may participate in all three stages, but the same authority channel must not be able to:

1. propose a consequential change
2. define or modify the validation criteria
3. issue the authorisation needed to enact that same change

If one actor can do all three, the separation is cosmetic.

For low-risk provisional context, automated validation is acceptable. For consequential persistence, Governance promotion, publication, sensitive-data access, destructive actions, or policy changes, the authorisation boundary must remain outside the proposing model's unilateral control.

## 3. Non-Governance can inform, not authorise

Classification metadata does not physically isolate a model from the semantic influence of the context it reads.

The authority rule is therefore explicit:

> Only Governance may grant or modify authority. Operating Context, Preferences, Ephemera, retrieved documents, external text, and other non-Governance context may inform reasoning but must not grant permission, weaken controls, change confirmation requirements, or override Governance.

Where the platform permits it:

- separate policy/control instructions from retrieved or provisional data
- preserve provenance and trust level on retrieved material
- treat untrusted memory as data, not executable policy
- avoid concatenating retrieved context into a privileged instruction channel

If the implementation flattens everything into one prompt stream, the application must still preserve the semantic distinction and accept the residual risk that non-authoritative text may influence generation.

## 4. Evidence for authority must be independent of the proposal

AI-authored reasoning can explain why a proposal exists. It is not independent evidence that the proposal should receive authority.

For consequential promotion, prefer evidence that can be identified outside the proposal itself, such as:

- an authoritative source document
- system or audit logs
- an approved policy record
- an authenticated user decision
- an independently generated application signal
- explicit human judgement

A model-generated justification may accompany that evidence, but must not be treated as its own proof.

## 5. Temporary must not renew itself into Keep

Temporary context can be renewed, but repeated renewal must not silently create de facto permanent persistence.

Each implementation should define one or more renewal triggers, for example:

- maximum cumulative duration
- maximum renewal count
- material scope change
- repeated retrieval after the original purpose has ended
- a change in sensitivity or authority impact

When a trigger fires, treat the item as a fresh persistence decision rather than inheriting prior Temporary approval indefinitely.

Temporary authority does not compound into permanent authority by neglect.

## 6. Roles and multi-actor authority

The model does not prescribe a universal RBAC scheme, but implementations should make the authorising principal identifiable.

At minimum, consequential records should be able to answer:

- who or what proposed the change?
- who or what validated it?
- who or what authorised it?
- what authority scope did that authoriser have?
- what evidence supported the decision?
- what version became effective?

Where multiple humans or policy actors can authorise changes, local precedence and conflict rules must be explicit. The model's default remains: if valid authority conflicts and precedence cannot be established, stop and escalate.

## 7. Recursive governance

Changes to the Governance rules of this operating model should pass through the same discipline they impose on governed context:

**PROPOSE → VALIDATE → AUTHORISE → VERSION → REVIEW**

A component proposing a governance change must not be able to unilaterally modify the mechanism that validates or authorises that same change.

Version control is evidence of change, not proof of proper authorisation. A diff without an authority decision is only a diff.

## 8. Residual risk remains

These boundaries reduce obvious self-authorisation and policy-poisoning paths. They do not turn this repository into a security product.

Real guarantees still depend on the surrounding identity, access-control, policy, prompt-assembly, storage, logging, deployment and review mechanisms of the implementation.
