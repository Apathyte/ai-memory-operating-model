# AI Memory, Governed

I dumped the working memory I had built up with an AI assistant.

Some of it was useful governance.
Some of it was operational context.
Some of it was preference.
Some of it had absolutely no business being persistent.

So I classified it.

This repository is a small, reusable operating pattern for doing the same thing without pretending there is one universal set of "AI principles."

## The four buckets

| Class | What it is | Default treatment |
|---|---|---|
| Governance | Rules the assistant must obey | Keep, review deliberately |
| Operating context | Facts needed to do useful work | Keep only while useful and appropriate |
| Preferences | How the human prefers to work | Keep when stable and genuinely helpful |
| Ephemera | Short-lived facts and one-off context | Remove or let expire |

The important bit is not the labels. The important bit is refusing to treat all memory as equally valuable, equally safe, or equally permanent.

## A few rules that survived the cut

- **Human authority:** availability of a tool is not permission to use it.
- **Preservation:** an improvement that destroys information is not automatically an improvement.
- **Provenance:** never invent where a fact, decision, or execution came from.
- **Evidence:** retrieve approved material before reconstructing it from memory.
- **Uncertainty:** unknown authority means stop, not infer permission.
- **Privacy:** operationally useful does not automatically mean appropriate for persistent memory.
- **Minimisation:** short-lived context should not quietly become identity.
- **Separation:** governance, facts, preferences, and transient context are different classes.

## Use it

1. Export or review the memory/context your assistant is using.
2. Remove secrets, personal data, customer-identifying detail, and irrelevant residue before sharing anything.
3. Classify the remainder.
4. Decide what deserves persistence.
5. Write explicit rules for the things that require a human gate.
6. Re-run the review periodically.

A blank template is included in [`memory-template.md`](memory-template.md).

## What this is not

This is not a universal governance framework and it is not a claim that these exact rules are correct for everyone.

It is a practical pattern: inspect what your assistant is carrying forward, classify it, remove what should not persist, and make authority explicit.

## Privacy warning

**Do not publish a raw memory dump.**

A useful internal memory can still contain personal information, confidential customer context, internal politics, infrastructure detail, security-adjacent facts, or accidental mosaics that identify people or organisations when combined.

Sanitise first. Publish second.

## License

The repository is released under the MIT License. See [`LICENSE`](LICENSE).
