---
name: design-dor-dod
description: >
  Generate or validate the Definition of Ready (DoR) before starting a UX/UI
  design task, and the Definition of Done (DoD) before calling it finished. Use
  when a design story is picked up, refined, or reviewed, triggers like
  "is this ready to design?", "write the DoR for this story", "define acceptance
  criteria for this screen", "is this design done?", or "check DoD before
  handoff". Enforces Ballast Lane's design intake and exit checkpoints so no task
  starts underspecified or ships incomplete.
---

# Design DoR / DoD

Apply a checkpoint at both ends of every design task. Do not design before DoR passes; do not
hand off before DoD passes.

## When to use
- A story enters refinement or is about to be picked up → build/validate the DoR.
- A design task is "finished" or heading to handoff → validate the DoD.
- Someone asks whether work is ready to start or ready to ship.

## Step 1: Identify the task and mode
Confirm the project mode (greenfield / redesign / existing design system) and the
platform + front-end framework, since these change what "ready" and "done" mean.

## Step 2: Definition of Ready (before designing)
Produce a checklist and mark each item ✅ present, ⚠️ drafted (assumption), or
❌ missing. If any core item is ❌, the task is NOT ready, state the blocker and
the smallest action to unblock it.

1. **Problem & goal**, user problem + business outcome this serves.
2. **Users & context**, who, device/context, moment in the journey.
3. **Scope**, explicitly in and out.
4. **Success criteria**, measurable/observable signal of success.
5. **Constraints**, platform, framework, existing DS/components, data,
   performance, legal/compliance, brand.
6. **Inputs available**, research, analytics, prior designs, content/copy,
   decisions already made.
7. **Dependencies**, what must exist first and who owns it.
8. **Accessibility & localization**, WCAG target (AA baseline), RTL, languages,
   dynamic type, contrast constraints.

For anything ⚠️/❌, either gather it, draft it and label it a hypothesis, or
escalate. Never silently proceed on a missing core item.

## Step 3: Definition of Done (before handoff)
Validate every item; the task is done only when all hold. Log any gap with a
concrete fix.

1. Solves the stated problem and meets the DoR success criteria.
2. All relevant states designed: default, hover, focus, active, disabled,
   loading, empty, error, success, overflow/edge.
3. Responsive behavior defined across breakpoints.
4. Built from the design system / tokens; deviations documented as formal
   exceptions.
5. Meets WCAG 2.2 AA (contrast, focus, keyboard, labels, reduced motion), verified, not assumed.
6. Motion/transitions specified where they carry meaning, with reduced-motion
   fallback.
7. Documentation & annotations complete; design rationale captured.
8. Content and copy finalized and reviewed (no placeholders / lorem ipsum).
9. Developer handoff ready: tokens and components map to the target front-end
   framework; assets exported; specs unambiguous.
10. Design QA self-review passed; review with engineering/PM done.
11. Open questions, assumptions, and risks explicitly listed.

## Output format
Return a compact, copy-pasteable checklist with status icons, a one-line verdict
(READY / NOT READY, or DONE / NOT DONE), and, when not passing, a short
"To unblock" list ordered by smallest effort first. Keep it usable in a ticket.

## Template
Use the bundled checklist `templates/dor-dod-checklist.md` as the fillable
starting point; copy it into the ticket or design file and mark each item.

## Notes
- Adapt depth to project mode and timeline, but never drop a core checkpoint silently.
- Pair with the `design-qa` skill for the detailed QA pass referenced in DoD #10.
