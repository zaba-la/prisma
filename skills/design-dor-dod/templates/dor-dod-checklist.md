# Intake / DoR / DoD Checklist

Project / feature: ____________________   Task / requirement: ____________________
Intake path: [ ] A, existing Figma or live product  [ ] B, requirements only
Operating mode: [ ] Lights out  [ ] Client in the loop
Platform: ____________   Front-end stack: ____________   Date: __________

Legend: [x] present · [~] assumption (logged in the register below) · [ ] missing

## Intake (against docs/intake-spec.md)

- [ ] 1. Jobs to be done, stated without reference to software.
- [ ] 2. How the user does it today (the workaround).
- [ ] 3. Users, plural, with role, frequency, expertise, device.
- [ ] 4. User stories with the "so that" clause intact.
- [ ] 5. Realistic data: real fields, ranges, volumes, plus the ugly cases.
- [ ] 6. Scope edges: what's explicitly out of this release.
- [ ] 7. Failure modes in the domain (useful, not required).
- [ ] 8. Hard constraints: stack, devices, accessibility target, localization,
      brand (useful, not required).
- [ ] 9. Success signal: how we'll know it worked (useful, not required).

Verdict: [ ] COMPLETE   [ ] COMPLETE WITH ASSUMPTIONS   [ ] BLOCKED
Blocked only applies to items 1, 3, or 5. If blocked, name which one and the
smallest action to unblock it: ______________________________________

### Assumption register
| # | Gap | Assumption made | Why | What changes if wrong |
|---|-----|------------------|-----|------------------------|
|   |     |                  |     |                        |

## Definition of Done (before handoff)

- [ ] 1. Solves the stated jobs to be done and meets the intake success signal.
- [ ] 2. All relevant states and responsive breakpoints designed.
- [ ] 3. Built from the design contract (deviations documented as exceptions).
- [ ] 4. Meets WCAG 2.2 AA, verified (contrast, focus, keyboard, labels, reduced motion).
- [ ] 5. Motion and transitions specified where they carry meaning.
- [ ] 6. Build brief acceptance checks pass, visual diff against the prototype attached.
- [ ] 7. Feel verdict run (client concept review, or Prisma's own fresh-context pass in lights out).
- [ ] 8. Documentation and design contract rationale complete.
- [ ] 9. Content and copy finalized (no placeholders).
- [ ] 10. Assumption register up to date with every open question and risk.

Verdict: [ ] DONE   [ ] NOT DONE
Gaps and fixes: __________________________________________________________
