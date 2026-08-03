# Intake Spec

Prisma does not run discovery. Requirements come in from upstream, and the
work of finding them (interviews, research, requirements gathering) happens
before Prisma is invoked. But a functional spec that tells engineers what to
build rarely tells a designer what to design: every requirement can be
present and the result still be unusable. This document is what Prisma asks
for instead, and it is a deliverable in its own right, publish it to whoever
originates requirements (a client, a PM, an upstream agent) so intake stops
being a guessing game.

## Required

- **Jobs to be done.** What the person is trying to accomplish, stated
  without reference to software. Skip this and the agent designs a feature
  list instead of an experience, the most common way agent-built UI fails:
  every requirement present, nothing usable.
- **How they do it today.** The workaround, the spreadsheet, the phone call,
  the paper form. The richest design input there is, and a functional spec
  never carries it.
- **Users, in the plural, with context of use.** Role, frequency, expertise,
  device. A daily power user and a monthly first-timer are two different
  products even when the feature list is identical.
- **User stories with the "so that" clause intact.** The "so that" is the
  only part of a user story that carries design intent, and it is the part
  that gets dropped in translation.
- **Realistic data.** Real fields, ranges, and volumes, plus the ugly cases:
  the 60-character name, the empty list, the 10,000-row table. Without this
  the prototype lies about what the product will look like under real
  conditions, and the build inherits the lie.
- **Scope edges.** What is explicitly not in this release. Design expands to
  fill silence, so an unstated edge becomes an invented one.

## Useful and cheap to get

- Failure modes that actually occur in the domain.
- Hard constraints: stack, devices, accessibility target, localization,
  brand.
- How anyone will know it worked (the success signal).

## Intake outcomes

Intake returns exactly one of three verdicts. This matters more than the
field list above.

1. **Complete.** Go.
2. **Complete with assumptions.** The normal case. Fill each gap, write it
   into a numbered **assumption register**, and keep moving. The register
   becomes part of the design contract and later doubles as the review
   agenda: here is what was assumed, here is what changes if any of it is
   wrong.
3. **Blocked.** Only three gaps qualify: no realistic data, no users, no jobs
   to be done. Nothing else blocks intake.

Default to assuming. A clarification questionnaire bouncing back to whoever
sent the requirements reads as the system not working, not as diligence. A
short, honest assumption register is also a credible thing to show a client
during a pitch: it states exactly what the factory needs in order to design
well.

## How this connects

- The assumption register produced here is a required section of the
  **design contract** (see the `design-system` skill).
- `design-dor-dod` runs this intake model at the start of every task and
  produces the Ready / Not Ready verdict from it.
- Which of the two intake paths applies next (an existing Figma file or
  live product, or requirements only) is decided in `agents/prisma.md` §1,
  after intake returns Complete or Complete with assumptions.
