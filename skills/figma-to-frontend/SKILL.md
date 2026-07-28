---
name: figma-to-frontend
description: >
  Convert a Figma design into production front-end code that maps to the
  project's existing framework and design system. Use when turning a Figma
  screen or component into code, triggers like "implement this Figma in
  React/shadcn", "turn this Figma into front-end", "build this screen from
  Figma", "code this component from the design". Enforces token- and
  component-mapping (no hardcoded values that a token owns), full state coverage,
  accessibility, and motion, so the build matches the design and the system.
---

# Figma → Front-end

Produce buildable, system-faithful code from a Figma design. The goal is
mechanical translation, not reinterpretation: every value should resolve to a
token or component that already exists (or a documented exception).

## Prerequisite: use the Figma tooling correctly
If the Figma MCP/plugin is connected, the `figma:figma-design-to-code` skill is
the MANDATORY prerequisite before calling `get_design_context`; load it first.
This skill layers Ballast Lane's mapping and quality rules on top of that flow.
If Figma access is not authorized, work from exported specs/screenshots the user
provides and note that live access would tighten fidelity.

## Step 1: Read the design and the target stack
Identify the front-end framework (React + shadcn/ui, Tailwind, MUI, etc.) and the
design system in play. Locate the codebase's theme config and existing
components (search for token config, component library imports).

## Step 2: Map before you write
- **Tokens:** map Figma variables/styles → the framework's theme (CSS custom
  properties, Tailwind config, MUI theme). Do not hardcode a color/spacing/radius
  that a token owns.
- **Components:** map each Figma component/variant → an existing code component
  and its real props (variant, size, slots). Reuse first; only build new when no
  component fits, and flag it as a system gap.
- **Layout:** translate auto-layout to the framework's layout primitives
  (fl/grid, spacing tokens), not magic numbers.

## Step 3: Implement
- Match structure to the component API so it reads like the rest of the codebase.
- Implement **all states**: default, hover, focus, active, disabled, loading,
  empty, error, success, overflow/edge.
- Implement responsive behavior across the design's breakpoints.
- Implement motion/transitions from spec (properties, duration, easing) using the
  stack's mechanism (CSS transitions, Tailwind utilities, Framer Motion), and
  honor `prefers-reduced-motion`.

## Step 4: Accessibility
Semantic HTML/roles, keyboard operability, visible focus states, labels/alt text,
contrast (4.5:1 text / 3:1 large text & UI), and target sizes (≥24×24 CSS px).

## Step 5: Verify
- Visual parity vs the design (spacing, type, color, radius, elevation).
- No rogue hardcoded values; everything resolves to tokens/components.
- All states and breakpoints present.
- Keyboard + screen-reader sanity check.
List any deviation from the design or system as a documented exception with a
reason.

## Output
Deliver the code files in the project's conventions, a short mapping table
(Figma token/component → code), and a list of exceptions/gaps to route back to
the design system. When the project uses **Storybook**, also deliver a story per
converted component, all variants and states, driven by controls (args), with
the accessibility addon, so it lands in the living component library. Pair with
`design-qa` for the post-build review.
