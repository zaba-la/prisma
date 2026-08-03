# Craft Floor

The craft floor is a growing list of machine-checked rules that catch the
small, repeated mistakes no principle document prevents on its own. It is
not designed upfront, it is built, one promoted correction at a time. It
lives at the platform level (installed once, shared by every project), not
per project, see [`tools.md`](tools.md) and §4 of `agents/prisma.md` for how
platform-level rules and per-project context divide.

## Starter set

These are examples to seed the floor, not a finished list. Adapt them to the
project's design contract, but keep the floor itself platform-level:

- No text under 14px.
- Sentence case, not Title Case, in UI copy.
- Scrims over imagery wherever text sits on a photo.
- No orphaned words in headlines.
- One type scale, no ad hoc font sizes.
- Motion stays consistent across sibling surfaces (same trigger, same
  duration/easing family).

## The promotion mechanism

The floor grows by one rule, immediately, the moment a pattern repeats:

> When a human repeats a correction, it becomes a machine-checked rule
> immediately. A third occurrence is a system failure, not a reminder.

This is worth more inside a factory than in a solo setup, because client
feedback is a high-volume, repeating correction stream. Without the
promotion loop, project 40 has exactly the same problems as project 1. With
it, every correction a human makes is the last time that human has to make
it.

## How it connects

- `design-qa` and the deterministic-detector layer check output against the
  current floor before anything reaches judgment critique, see the "Layer
  the quality work by cost" note in `agents/prisma.md` §7.
- `design-system` treats the floor as a constraint on the design contract:
  a token or component that would violate the floor gets flagged before it
  ships, not after.
- New floor rules are proposed the same way any system change is: through
  governance, with the repeated correction as the rationale.
