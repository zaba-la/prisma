---
name: design-system
description: >
  Create, audit, extend, or consume a design system for a software product. Use
  when the work involves design tokens, component libraries, theming, or system
  governance, triggers like "set up a design system", "audit our design
  system", "define our design tokens", "add a component to the system", "is this
  in the system already?", or "map our tokens to Tailwind/shadcn". Handles all
  three project modes (greenfield, redesign, existing DS) and keeps design 1:1
  with the front-end framework.
---

# Design System

Treat the design system as a product with foundations → primitives → patterns.
Reuse before creating; propose system changes through governance, never one-offs.

## Step 1: Determine the situation
Pick the path that matches the project mode:
- **Create (greenfield):** no system yet → build foundations alongside the first
  real screens; don't gold-plate before screens exist.
- **Audit / extend (redesign or maturing DS):** inventory what exists, find
  gaps and inconsistencies, extend deliberately.
- **Consume (existing DS):** use the system faithfully; document any needed gap
  as a formal proposal.

Confirm the front-end framework (e.g. React + shadcn/ui, Tailwind, MUI, SwiftUI)
so the system maps 1:1 to code.

## Step 2: Tokens (source of truth), starting from the brand
Tokens must originate from the brand, not arbitrary values. Before defining them,
gather the brand foundation: identity/brand guidelines, logo and clear-space,
core palette, typefaces, shape language, imagery style, motion personality, and
tone of voice. If no brand exists yet, flag it and agree on a minimal brand
direction first, don't invent one silently.

Then define in layers so theming is clean:
- **Primitive tokens:** the brand encoded, brand palette, type scale from the
  brand typefaces, spacing, radius/border (brand shape language), shadow,
  z-index, motion (duration/easing reflecting brand personality), breakpoints.
- **Semantic / alias tokens:** meaning-based (e.g. `color.bg.surface`,
  `color.text.default`, `color.action.primary`) referencing primitives.
- **Component tokens:** per-component values referencing semantic tokens.
Support light/dark and brand theming through the semantic layer. Map tokens to
the framework's theme config (CSS custom properties, Tailwind `theme.extend`,
MUI theme). Never leave a value hardcoded that a token should own.

## Step 3: Components
For each component define: anatomy, variants, states (default, hover, focus,
active, disabled, loading, empty, error), props/API, do's and don'ts, and
accessibility behavior (roles, keyboard, focus, labels). Name variants/props to
mirror the framework's actual API so translation is mechanical (e.g. a Button's
variant set matches shadcn/ui `variant`/`size`).

## Step 3b: Living library (Storybook)
When the team uses Storybook, it is a first-class deliverable of the design
system, not an afterthought. For each component ship a story that covers:
- every variant and size, driven by controls (args) so reviewers can toggle them;
- every state (default, hover, focus, active, disabled, loading, empty, error);
- usage docs (MDX/autodocs): anatomy, do's and don'ts, props/API;
- the accessibility addon enabled, and interaction tests for key behaviors.
Bind stories to the same tokens as the app (no hardcoded values), and keep them
in sync with the design source so Storybook is the single living reference
shared by design and engineering, and a natural surface for design QA.

## Step 4: Audit checklist (when auditing/extending)
- Inventory components and tokens; list duplicates and inconsistencies.
- For each gap, decide: true gap (new/extended component) vs misuse (pattern
  already exists). Prefer extension over addition; addition over one-off.
- Check coverage of states, responsive rules, theming, and accessibility.
- Flag hardcoded values that should be tokens.

## Step 5: Governance & documentation
Document usage guidelines, content/voice rules, and the process for proposing,
reviewing, and adding a component. Every change needs rationale, affected
surfaces, and a migration note. Keep a changelog.

## Output
Deliver the artifact appropriate to the request: a token spec (with framework
mapping), a component spec, an audit report with prioritized findings, a
governance/contribution note, or, when the team uses Storybook, the component
library in Storybook (one story per component with variants, states, controls,
docs, and accessibility). Be explicit about exceptions and their reasons.

## Notes
- Brand is the foundation: tokens encode the brand, and every phase (UI, motion,
  content/voice) should feel like the same brand. Verify brand colors meet
  contrast targets; resolve conflicts at the semantic layer, not by dropping the
  brand.
- Consuming an existing DS: deviations must be formal, documented exceptions
  routed to the system owners, never silent divergence.
- Pair with `figma-to-frontend` for token/component extraction from Figma, and
  with the `brand-applicator` skill when producing brand-styled deliverables
  (decks, docs, carousels, UI) from the defined brand.
