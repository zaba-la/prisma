---
name: design-qa
description: >
  Run a structured design quality review, before handoff (design self-review)
  and after implementation (design vs. build review). Use when checking a design
  or a built UI for quality, triggers like "QA this design", "review this
  screen before handoff", "does the build match the design?", "design review",
  or "check this against the mockups". Produces a severity-ranked issue log tied
  to specific screens/components, covering states, responsiveness, tokens,
  accessibility, content, and motion.
---

# Design QA

Two passes: pre-handoff (design vs. intent) and post-implementation (build vs.
design). Both produce an actionable, severity-ranked issue log.

## Choose the pass
- **Pre-handoff self-review:** the design is "done" and about to go to
  engineering.
- **Post-implementation review:** the feature is built and needs to match the
  design and system.

## Pre-handoff checklist
- **States:** default, hover, focus, active, disabled, loading, empty, error,
  success, overflow/edge, all designed.
- **Responsive:** behavior defined across breakpoints (smallest and largest
  meaningful widths, not just one).
- **System fidelity:** tokens/components used correctly; no rogue hardcoded
  values; deviations documented as exceptions.
- **Accessibility:** contrast (4.5:1 text / 3:1 large text & UI), logical focus
  order, visible focus states, target sizes (≥24×24 CSS px, ideally 44×44),
  labels/alt text, keyboard operability, clear error identification.
- **Content:** real content, not lorem ipsum; copy reviewed.
- **Motion:** specified where meaningful, with a reduced-motion fallback.

## Post-implementation checklist
- **Visual parity:** spacing, type, color, radius, elevation match tokens.
- **Interaction & motion:** match spec, including interrupt/reverse behavior.
- **State & responsive coverage:** verified in the real build, not just design.
- **Accessibility in the build:** verify with keyboard and a screen reader, not
  visually alone; check contrast on rendered output.
- **Regressions:** nothing previously working was broken (esp. in redesigns).

## Severity scale
- **Blocker**, breaks the task, inaccessible, or ships wrong data/behavior.
- **Major**, clear deviation from design/system or a real usability problem.
- **Minor**, noticeable but non-blocking inconsistency.
- **Polish**, nice-to-have refinement.

## Output
Return an issue log as a table: `# | Screen/Component | Issue | Severity |
Expected vs Actual | Recommended fix`. Group by severity, lead with blockers,
and end with a one-line verdict (PASS / PASS WITH FIXES / FAIL). Tie every issue
to a specific location so it's fixable without a meeting.

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
- Pair with `design-dor-dod` (QA is DoD item #10), `accessibility-audit` for a
  deep WCAG pass, and `heuristic-evaluation` for an expert usability review, QA checks states, system fidelity, and build parity; heuristic evaluation
  judges usability against principles.
