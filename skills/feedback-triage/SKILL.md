---
name: feedback-triage
description: >
  Route end-of-run feedback in lights-out mode, where the client only sees
  the finished product and feedback comes back mixed, to the right owner.
  Use when a batch of feedback needs sorting before anyone acts on it,
  triggers like "triage this feedback", "sort this round of feedback", "what
  do we do with this client response", or "route these notes". Every item
  goes to exactly one of four places: a design contract change, a prototype
  change, a build defect, or a new requirement. Without this step,
  lights-out mode drowns in its own feedback.
---

# Feedback Triage

Lights-out mode has zero human design gates, so nothing catches a wrong
direction until the client sees the finished product. When feedback comes
back, it is never scoped to one thing, it is design opinion, product
requests, bug reports, and new asks, all mixed together in one message.
Acting on it unsorted is how a single round of feedback turns into
rework across every part of the pipeline at once. This skill exists to sort
it first.

## When to use
Only in lights-out mode (`agents/prisma.md` §10), at the end of a run, once
feedback comes back. Client-in-the-loop mode doesn't need this: its feedback
is already scoped to the design contract by the concept-review rules in
`agents/prisma.md` §10.

## Step 1: Split the batch into atomic items
Break the feedback into individual, single-topic items before routing
anything. A sentence that raises two issues becomes two items. Don't route a
paragraph, route each claim inside it.

## Step 2: Route each item to exactly one owner
Every item goes to exactly one of these four places. If an item seems to fit
two, split it further, it wasn't atomic yet.

- **Design contract change.** The complaint is about tokens, a component,
  motion, or the stated audience/feel, something that should change for
  every screen that uses it, not just the one the client looked at. Route to
  `design-system`.
- **Prototype change.** The complaint is about one specific flow or screen's
  behavior, not a system-wide rule. Route to `frontend-prototype`.
- **Build defect.** The build doesn't match the approved prototype or design
  contract, this is what `design-qa`'s visual diff exists to catch, and if
  QA already flagged it, link the existing finding instead of duplicating
  it. Route as a recommendation to the build agent, not a block.
- **New requirement.** The item asks for something outside the original
  intake's scope edges. This isn't a design or build problem, it's new
  scope. Route it back through `design-dor-dod` as a fresh intake item, it
  needs its own Ready verdict, not a quiet addition to the current one.

## Step 3: Attach severity and evidence
For design contract and prototype items, attach severity the same way
`design-qa` does (blocker / major / minor / polish). For build defects,
attach the visual diff if one exists. For new requirements, note whether
they're in tension with an existing scope edge from the assumption
register, if so, flag the conflict explicitly rather than silently
expanding scope.

## Step 4: Confirm nothing was silently dropped
Every item from the original batch appears in exactly one row of the
output. An item that doesn't fit cleanly is a signal the routing categories
above need to be re-examined, not a reason to drop it.

## Output
A triage log: `# | Original feedback item | Route (contract / prototype /
build defect / new requirement) | Severity | Evidence / linked finding |
Notes`. Group by route so each downstream owner can work from their own
slice without re-reading the whole batch.

## Template
Use the bundled `templates/feedback-triage-log.csv` to record each item with
its route, severity, and evidence.

## Notes
- This skill only sorts, it doesn't resolve. Resolution happens in whichever
  skill the item was routed to.
- A pattern of the same item recurring across runs is craft-floor material,
  see `docs/craft-floor.md`, promote it instead of re-triaging it every
  time.
