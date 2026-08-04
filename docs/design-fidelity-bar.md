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
  semantic role) is a deviation, not just a hardcoded value is. **Token
  correctness is categorical, not a matter of visual closeness.** A wrong
  token that is visually adjacent to the right one (a neighboring step in
  the same palette) is exactly as much a deviation as a token that is
  wildly off, the severity does not soften with proximity, see the severity
  mapping below. A design contract exists so "close enough" stops being a
  valid judgment; if a rebrand later moves that palette step, a near-miss
  value drifts silently while a correctly-tokened one updates for free.
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

1. **Capture.** Two things per state, not one: a screenshot of the prototype
   and the build at the same named viewports, same route and state, same
   seeded data, and a computed-style/token manifest (the resolved CSS
   variables and rendered values actually used) for that same state. The
   manifest is what the structural token check below reads, the screenshot
   is what the perceptual diff reads.
2. **Diff.** Two mechanisms, not one, matched to what each is good at:
   - **Structural, for tokens.** Compare the captured manifest's values
     against the exact token values in the design contract. Exact match or
     not, no tolerance band, this is deterministic and byte-comparable, the
     same class of evidence as a passing test.
   - **Perceptual, for everything else.** A tolerance-based diff for layout,
     spacing, and composition, where "close enough" is a real category and
     anti-aliasing/font-rendering noise has to be tolerated. Compare per
     region, not only the whole page, so a small real deviation is not
     diluted by a mostly-matching screen.
3. **Severity.**
   - **Blocker:** a token or spacing deviation on a first-impression
     surface, or a required state missing entirely.
   - **Major:** a token or spacing deviation elsewhere (including a
     near-miss, visually adjacent wrong token, see above), or a state
     present but visibly wrong.
   - **Minor:** a real, non-token difference above the noise floor but
     below what a user would notice unprompted (a sub-pixel layout shift, a
     shadow blur radius off by a fraction). A wrong token is never Minor,
     regardless of how close it looks, see above.
   - **Polish:** cosmetic only.
4. **Evidence required.** Every finding carries the diff image. A finding
   without an attached comparison image does not count, per the existing
   rule in `design-qa`.

The exact tolerance numbers, diff tooling, and per-region thresholds are
left open here on purpose. Fix them from what the pilot's seeded deviations
actually show, not from a guess made before anything has run against a real
build.

### Why the structural/perceptual split matters

A near-miss token is the hardest input for a pure perceptual diff: loosen
the tolerance enough to survive rendering noise and it stops catching a
one-step-off palette substitution, tighten it enough to catch that and it
drowns in the same noise. No single tolerance satisfies both, which is why
the split above exists rather than one diff mechanism doing everything.

Two consequences worth keeping in view. First, this boundary was derived
twice, independently, from opposite ends: once here, from the severity
ladder (a wrong token is never "sort of right," so it can never fall to a
perceptual "close enough"), and once from the evidence side (a probe typed
as visual-equivalence must not be allowed to satisfy a token-correctness
item). Two independent routes landing on the same partition is a much
stronger signal that it is real than either argument alone. Second, it
shrinks the hard part of tolerance calibration: the structural half is
exact and needs no threshold at all, so the seeded-mismatch pilot's
tolerance tuning (see below) only has to cover layout and spacing, not the
near-miss token case, which was the least tunable input in the whole bar.

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

- one off-token color, including at least one near-miss (a neighboring
  palette step, not just an obviously wrong one), to exercise the
  structural check rather than the perceptual tolerance
- one spacing value off the scale
- one missing state (an empty state omitted, for instance)
- one off-breakpoint layout issue

Run the fidelity check against the seeded build and record two numbers,
scoped to what each mechanism actually needs to prove:

- **Structural (tokens):** catch rate should be exact, every seeded token
  deviation flagged, including the near-miss, since there is no tolerance
  band to get wrong. Anything missed here is a bug in the check, not a
  calibration question.
- **Perceptual (layout/spacing), catch rate and false-positive rate:** how
  many of the seeded layout/spacing deviations were flagged, and what got
  flagged that was not a real deviation (anti-aliasing, font rendering,
  one-pixel shifts), at what tolerance threshold those disappear.

Adjust the perceptual tolerance and the severity mapping above based on
these results, and version this document afterward. An unexercised
verification path is presumed broken until it has caught something real.
