---
name: accessibility-audit
description: >
  Audit a design or built UI against WCAG 2.2 AA and produce prioritized
  remediation. Use for any accessibility check, triggers like "is this
  accessible?", "run a WCAG audit", "check contrast and keyboard access",
  "a11y review", "make this screen accessible", or when a client requires an
  accessibility conformance level. Covers perceivable, operable, understandable,
  and robust criteria, plus reduced motion, focus, and assistive-technology
  behavior. Escalates when the context is regulated (healthcare, finance,
  public sector) and a higher bar (AAA / legal conformance) may apply.
---

# Accessibility Audit (WCAG 2.2 AA)

Assess a design or implementation against WCAG 2.2 AA and return an actionable,
prioritized fix list. Verify, don't assume, and test with real assistive
technology when auditing a build.

Run this as early as possible, it belongs primarily in the cheap layers of
QA (creation-time context and the deterministic detector, see
`agents/prisma.md` §7), not as a phase-5 discovery. By the time an
accessibility gap reaches judgment critique it's remediation, not
prevention. When you do run this as judgment critique, apply the same
fresh-context rule as `design-qa`: no visibility into the design
conversation, briefed only by the artifact.

## Step 0: Set the bar
Confirm the target conformance level. AA is the baseline. Raise the question if
the project is regulated (healthcare, finance, government) or the client
specifies AAA or a legal standard (e.g. ADA, Section 508, EN 301 549, EAA), the
criteria and evidence needed change.

## Step 1: Perceivable
- Text alternatives for non-text content (alt text, icon labels).
- Contrast: 4.5:1 for normal text, 3:1 for large text and UI components/graphics.
- Don't convey information by color/shape/position alone.
- Content reflows at 320px width and 200-400% zoom without loss.
- Meaningful reading and content order.

## Step 2: Operable
- Full keyboard operability; no keyboard traps.
- Visible, non-obscured focus indicator (WCAG 2.2: Focus Not Obscured).
- Logical focus order.
- Target size ≥24×24 CSS px (WCAG 2.2 minimum; prefer 44×44).
- No content that flashes more than 3×/second.
- Dragging actions have a single-pointer alternative (WCAG 2.2).
- Time limits adjustable; motion from device sensors has alternatives.

## Step 3: Understandable
- Clear labels and instructions; programmatic label ↔ visible text match.
- Errors identified in text, with suggestions and prevention on critical actions.
- Consistent navigation and naming.
- Language of page/parts set.
- Consistent help placement and no redundant re-entry of info (WCAG 2.2).

## Step 4: Robust
- Valid, semantic markup; correct roles/states/properties (ARIA only when native
  semantics fall short).
- Name, role, value exposed for custom components.
- Status messages announced without stealing focus.

## Step 5: Motion & cognitive
- Honor `prefers-reduced-motion`; provide reduced/no-motion fallback.
- Avoid parallax/auto-playing motion that can't be paused.

## How to test
- **Design:** contrast checks on tokens/states, focus-order annotation, target
  sizes, text alternatives specified.
- **Build:** keyboard-only walkthrough; screen reader (VoiceOver/NVDA); automated
  pass (axe/Lighthouse) as a floor, not proof; zoom/reflow at 400%.

## Output
Issue log: `# | Location | WCAG criterion (SC) | Level | Severity | Finding |
Fix`. Group by severity (Blocker / Major / Minor), map each to its success
criterion, and end with a conformance verdict and the top fixes. Note where
manual testing is still required to confirm.

## Template
Use the bundled `templates/wcag-aa-checklist.md` to walk the POUR criteria with
checkboxes and record findings in the table at the bottom.
