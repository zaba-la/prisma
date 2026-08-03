---
name: design-dor-dod
description: >
  Run intake against the intake spec to produce a Ready / Not Ready verdict
  before starting a UX/UI design task, and validate the Definition of Done
  (DoD) before calling it finished. Use when a design task or requirements
  handoff arrives, triggers like "run intake on this", "is this ready to
  design?", "write the DoR for this task", "is this design done?", or "check
  DoD before handoff". Defaults to assuming over asking: intake returns
  Complete, Complete with assumptions, or Blocked, and only three gaps ever
  block (no realistic data, no users, no jobs to be done).
---

# Design DoR / DoD

Two decision gates, few, named, each paired with a rendered checklist, not a
quality gate. Do not design before intake passes; do not hand off before DoD
passes.

## When to use
- A requirements handoff arrives, or a task enters refinement → run intake.
- A design task is "finished" or heading to handoff → validate the DoD.
- Someone asks whether work is ready to start or ready to ship.

## Step 1: Run intake against the intake spec
Check the handoff against `docs/intake-spec.md`. Required: jobs to be done
(no reference to software), how the user does it today, users in the plural
with context of use (role, frequency, expertise, device), user stories with
the "so that" clause intact, realistic data (including the ugly cases: long
names, empty lists, huge tables), and scope edges. Useful and cheap: known
failure modes, hard constraints (stack, devices, accessibility,
localization, brand), and how success will be measured.

## Step 2: Return one of three verdicts
Never a fourth option, and never a clarification round back to whoever sent
the requirements.

1. **Complete.** Every required item present. Go.
2. **Complete with assumptions.** The normal case. For each gap, write a
   numbered entry in the **assumption register**: what's assumed, why, and
   what changes if it's wrong. Fold the register into the design contract
   and keep moving.
3. **Blocked.** Only three gaps qualify: no realistic data, no users, no
   jobs to be done. State exactly which of the three is missing and the
   smallest action that would unblock it. Nothing else blocks intake,
   everything else becomes an assumption.

## Step 3: Confirm platform, path, and mode
Once intake passes, confirm the platform + front-end framework, which
intake path applies (`figma-intake` if a Figma file or live product exists,
otherwise requirements-only), and the operating mode (lights out or client
in the loop, a commercial decision, never assumed silently). These come from
`agents/prisma.md` §1 and shape what "ready" and "done" mean for this task.

## Step 4: Definition of Done (before handoff)
Validate every item; the task is done only when all hold. Log any gap with a
concrete fix.

1. Solves the stated jobs to be done and meets the success signal from
   intake.
2. All relevant states designed: default, hover, focus, active, disabled,
   loading, empty, error, success, overflow/edge.
3. Responsive behavior defined across breakpoints.
4. Built from the design contract; deviations documented as formal
   exceptions.
5. Meets WCAG 2.2 AA (contrast, focus, keyboard, labels, reduced motion),
   verified, not assumed.
6. Motion/transitions specified where they carry meaning, with
   reduced-motion fallback.
7. The build brief's acceptance checks pass, and a visual diff against the
   prototype is attached, not just described (see `design-qa`).
8. The feel verdict has run: the client's concept review in
   client-in-the-loop mode, or Prisma's own fresh-context pass in lights
   out.
9. Documentation and the design contract's rationale captured.
10. Content and copy finalized and reviewed (no placeholders / lorem ipsum).
11. Open questions, assumptions, and risks explicitly listed in the
    assumption register.

## Output format
Return a compact, copy-pasteable checklist with status icons, a one-line
verdict (Complete / Complete with assumptions / Blocked, or DONE / NOT DONE),
and, when not passing, a short "To unblock" list ordered by smallest effort
first. Keep it usable in a ticket.

## Template
Use the bundled checklist `templates/dor-dod-checklist.md` as the fillable
starting point; copy it into the ticket or design contract and mark each
item.

## Notes
- Default to assuming, not asking. A clarification round reads as the
  pipeline not working; a labeled assumption keeps it moving and doubles as
  the review agenda later.
- Adapt depth to intake path and operating mode, but never drop the
  three-outcome model or the blocking-reason limit.
- Pair with `design-qa` for the detailed QA pass referenced in DoD #7, and
  with `feedback-triage` when a lights-out run's feedback needs routing back
  into a new DoR cycle.
