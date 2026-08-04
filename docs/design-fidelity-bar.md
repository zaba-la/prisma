# Design Fidelity Bar (Provisional)

**Status: provisional, written before the pilot.** This exists so there is
something concrete to be wrong about once the pilot runs, not because it is
expected to survive unchanged. Revise it after the pilot's seeded-mismatch
run (see the bottom of this document) rather than treating it as settled.

This is the single artifact that answers "what does faithful to the design
mean, and how do we measure it." It pulls together what already lives split
across the design contract (the "who it's for and how it should feel"
section, see `agents/prisma.md` §4) and the visual-diff spec in `design-qa`.

## What "faithful to the design" means

- **Token fidelity.** Every color, spacing, radius, and type value in the
  build resolves to a token in the design contract, or is a documented
  exception. A value that resolves to the wrong token (off-scale, wrong
  semantic role) is a deviation, not just a hardcoded value is.
- **State completeness.** Every state named in the prototype and the build
  brief (default, hover, focus, active, disabled, loading, empty, error,
  success, overflow) exists in the build. A missing state is a deviation,
  not a stylistic note.
- **Layout and visual match.** Spacing, alignment, and composition match the
  prototype at each named breakpoint within the tolerance below.
- **Content match.** Real content is present, no placeholder or lorem ipsum
  left in, and copy matches the prototype unless a change is flagged as a
  deliberate content or localization decision.
- **Motion, partially covered here.** Trigger, duration, and easing should
  match the design contract's motion tokens, but a static screenshot diff
  cannot fully prove this. Treat motion correctness as a judgment call for
  `review-animations` (see `docs/tools.md`) until the pilot tells us whether
  a frame-sampled or video capture belongs in this bar too.
- **Not covered here: the feel verdict.** Whether the result feels right,
  brand personality, taste, is a separate judgment gate (the client's
  concept review, or Prisma's own fresh-context pass in lights-out mode, see
  `agents/prisma.md` §10). This bar does not claim to measure feel.

## How we measure it

1. **Capture.** Screenshot the prototype and the build at the same named
   viewports, same route and state, same seeded data.
2. **Diff.** A perceptual diff, not a naive pixel-exact comparison, with a
   tolerance threshold for anti-aliasing and font-rendering noise. Compare
   per region, not only the whole page, so a small real deviation is not
   diluted by a mostly-matching screen.
3. **Severity.**
   - **Blocker:** a token or spacing deviation on a first-impression
     surface, or a required state missing entirely.
   - **Major:** a deviation elsewhere, or a state present but visibly wrong.
   - **Minor:** a difference above the noise floor but below what a user
     would notice unprompted.
   - **Polish:** cosmetic only.
4. **Evidence required.** Every finding carries the diff image. A finding
   without an attached comparison image does not count, per the existing
   rule in `design-qa`.

The exact tolerance numbers, diff tooling, and per-region thresholds are
left open here on purpose. Fix them from what the pilot's seeded deviations
actually show, not from a guess made before anything has run against a real
build.

## Advisory internally, no external claim yet

- **Internally, every finding here is advisory:** severity-tagged, escalates
  to a human if it survives, never blocks a build agent. This does not
  change what `design-qa` already does.
- **Externally, no client-facing "design fidelity verified" claim is made
  against this bar until the pilot has validated it.** A design claim
  without a measured check behind it is exactly the kind of gap that would
  cost credibility, so this bar stays internal-only until it has caught
  something real.

## Validating this bar: the seeded-mismatch pilot

A pilot where the check simply passes proves nothing, it only shows the
screenshots matched. Before the pilot build runs, plant known deviations,
for example:

- one off-token color
- one spacing value off the scale
- one missing state (an empty state omitted, for instance)
- one off-breakpoint layout issue

Run the fidelity check against the seeded build and record two numbers:

- **Catch rate:** how many of the seeded deviations were flagged, and at
  what severity.
- **False-positive rate:** what got flagged that was not a real deviation
  (anti-aliasing, font rendering, one-pixel shifts), and at what tolerance
  threshold those disappear.

Adjust the tolerances and severity mapping above based on these results, and
version this document afterward. An unexercised verification path is
presumed broken until it has caught something real.
