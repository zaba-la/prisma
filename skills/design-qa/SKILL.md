---
name: design-qa
description: >
  Run a structured, advisory design quality review, before handoff (design
  self-review) and after implementation (build vs. prototype, proven with a
  visual diff, not a description). Use when checking a design or a built UI
  for quality, triggers like "QA this design", "does the build match the
  prototype", "diff this build against the design", "design review", or
  "check this against the mockups". Findings are severity-tagged
  recommendations, never a block on a build agent; a violation that
  survives escalates to a human. Must run in a fresh context with no
  visibility into the design conversation.
---

# Design QA

Two passes: pre-handoff (design vs. intent) and post-implementation (build
vs. prototype). Both produce an actionable, severity-ranked issue log of
recommendations, never a gate that blocks a build agent's output.

## Run this with fresh context
Whoever runs this checklist does so in a session with no visibility into the
conversation that produced the design, briefed only by the artifact (the
prototype, the build, and screenshots). A critic that shares context with
the work it's checking optimizes for agreeing with itself, not for finding
problems. This applies to both passes below.

## Where this sits in the cost-ordered layers
This skill is the third and most expensive of three QA layers (see
`agents/prisma.md` §7): creation-time context (the design contract and build
brief are complete enough that a build agent doesn't need correcting),
a deterministic detector (a script, no model, checking every UI file edit
against `docs/craft-floor.md`, non-blocking), and, last, this judgment
critique. If a finding here recurs, that's a signal the craft floor is
missing a rule, promote it (see `docs/craft-floor.md`) rather than relying
on catching it here every time.

## Choose the pass
- **Pre-handoff self-review:** the design is "done" and about to become a
  build agent's contract.
- **Post-implementation review:** a build exists and needs to match the
  prototype and the design contract.

## Pre-handoff checklist
- **States:** default, hover, focus, active, disabled, loading, empty, error,
  success, overflow/edge, all designed.
- **Responsive:** behavior defined across breakpoints (smallest and largest
  meaningful widths, not just one).
- **Contract fidelity:** tokens/components used correctly; no rogue hardcoded
  values; deviations documented as exceptions.
- **Accessibility:** contrast (4.5:1 text / 3:1 large text & UI), logical focus
  order, visible focus states, target sizes (≥24×24 CSS px, ideally 44×44),
  labels/alt text, keyboard operability, clear error identification.
- **Content:** real content, not lorem ipsum; copy reviewed.
- **Motion:** specified where meaningful, with a reduced-motion fallback.

## Post-implementation checklist
- **Visual diff, not a sentence.** Screenshot the prototype and the build at
  matching viewports and attach the comparison image. A QA claim without a
  comparison image is not evidence. See `docs/tools.md` for the recommended
  tooling: agent-browser for the render/screenshot loop, Playwright for
  repeatable acceptance checks against the build brief in CI. Score the diff
  against `docs/design-fidelity-bar.md`, the provisional definition of what
  "faithful to the design" means and where it becomes a client-facing claim
  versus stays internal-only.
- **Interaction & motion:** match spec, including interrupt/reverse behavior.
- **State & responsive coverage:** verified in the real build, not just design.
- **Accessibility in the build:** verify with keyboard and a screen reader, not
  visually alone; check contrast on rendered output.
- **Build brief acceptance checks:** run every check the build brief listed as
  self-runnable; log which passed and which didn't.
- **Regressions:** nothing previously working was broken (esp. in redesigns).

## The feel verdict
Everything above proves function and parity. It doesn't prove the result
feels right, no agent judges that alone. That's a separate gate: the
client's concept review in client-in-the-loop mode, or Prisma's own
fresh-context pass before delivery in lights-out mode (see
`agents/prisma.md` §10). Don't let a PASS on this checklist stand in for it.

## Severity scale
- **Blocker**, breaks the task, inaccessible, or ships wrong data/behavior.
- **Major**, clear deviation from the design contract or a real usability problem.
- **Minor**, noticeable but non-blocking inconsistency.
- **Polish**, nice-to-have refinement.

## Output
Return an issue log as a table: `# | Screen/Component | Issue | Severity |
Expected vs Actual | Recommended fix`. Group by severity, lead with blockers,
attach the visual diff image for the post-implementation pass, and end with a
one-line verdict (PASS / PASS WITH FINDINGS / FAIL). Every issue is a
recommendation with a severity, not an instruction to stop; a Blocker that
isn't addressed after being surfaced is what triggers a human escalation,
this skill never halts the build agent itself.

## Template
Use the bundled `templates/qa-issue-log.csv` to record findings by severity, tied
to a specific screen or component, with expected vs actual and status tracking.

## Notes
- The state coverage you verify here is defined once in the Structure phase: use
  the per-flow / per-screen **state inventory** from `ia-user-flows` as the
  checklist, every state named there must be designed and built.
- When the project uses **Storybook**, use it as the primary QA surface: review
  every component's variants and states via controls, run the accessibility
  addon and interaction tests, and check visual-regression snapshots if
  configured.
- Pair with `design-dor-dod` (QA is DoD item #7), `accessibility-audit` for a
  deep WCAG pass (run it early, in the cheaper layers, when possible), and
  `heuristic-evaluation` for an expert usability review. QA checks states,
  contract fidelity, and build parity; heuristic evaluation judges usability
  against principles.
- In lights-out mode, findings this skill surfaces are also raw material for
  `feedback-triage` if they arrive mixed with other end-of-run feedback.
