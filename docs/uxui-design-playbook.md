# Ballast Lane: UX/UI Design Playbook

A shared handbook for how we do product design at Ballast Lane. It exists so that
designers, engineers, and product managers work from the same definitions,
rituals, and quality bar, whether we're building a product from zero, redesigning
a legacy one, or contributing to an established design system.

This playbook is the human-readable companion to **Prisma**, our UX/UI Design
Agent, and its skills. Prisma applies these same standards inside Cowork; this
document is what the team reads, references in tickets, and uses to onboard new
members.

---

## 1. What we believe

Design at Ballast Lane is accountable for outcomes, not just screens. A few
principles guide every engagement:

**Outcomes over deliverables.** Every artifact traces back to a user problem and
a business goal. If we can't state the "why," we find it before we make pixels.

**Evidence before opinion.** We prefer data, research, and heuristics over taste.
When we rely on taste, we say so.

**Constraints are inputs, not blockers.** Platform, tech stack, timeline, team
maturity, and accessibility requirements shape the design from the start.

**Brand is the foundation, not the veneer.** The design system starts from the
brand, its identity, personality, and voice. Tokens encode the brand rather than
being chosen arbitrarily and styled later, and every phase should feel like the
same brand.

**Systematize by default.** We reuse before we create. A new pattern either fits
the system or is proposed as a system change, never a silent one-off.

**Accessibility is not optional.** WCAG 2.2 AA is our baseline on every project.
Regulated work (healthcare, finance, public sector) may require more, and we raise
that early.

**Design for handoff from day one.** If engineering can't build it unambiguously,
the design isn't done.

**Small, reviewable increments.** Design ships in the team's sprint cadence, thin
vertical slices over big-bang reveals.

---

## 2. Three project modes

Before design starts, we classify the engagement, because it changes where we put
our effort.

**Greenfield (0-to-1).** No product, no system. We emphasize discovery, problem
framing, information architecture, and establishing design foundations (tokens,
primitives) alongside the first real flows. We build the system as we build the
product, we don't gold-plate it before there are screens to justify it.

**Redesign / modernization.** A product exists and is being reworked. We emphasize
auditing what's there (heuristics, content, UX debt), understanding why current
patterns exist, planning the migration, and avoiding regressions. We map old → new
so nothing critical gets dropped.

**Existing design system.** A defined system or component library is in place. We
emphasize consuming it faithfully, identifying genuine gaps, and proposing
additions through the system's governance. Our job is consistency and
contribution, not reinvention.

For every mode we confirm the platform(s), the front-end framework in play (e.g.
React + shadcn/ui, Tailwind, MUI, SwiftUI), and the design tool (Figma by
default). These define what "buildable" means.

---

## 3. The design lifecycle

We adapt depth to the mode and timeline, but we never skip a phase silently, if
we compress or drop one, we say why.

**Discovery & framing.** Clarify the business objective, constraints, and success
metrics. Map stakeholders and decisions already made. **Decide the front-end
stack here**, based on platform and project type, we recommend the
framework/library and settle it with engineering, because tokens and components
map to the chosen stack (a web dashboard leans to shadcn/ui + Tailwind; a native
mobile app to SwiftUI + Apple HIG or Jetpack Compose + Material 3). Frame the
problem (jobs-to-be-done, "How might we…") and name the riskiest assumptions to
validate first.

**Research.** Choose the lightest method that answers the question, stakeholder
and user interviews, surveys, analytics review, support-ticket mining,
competitive analysis, and heuristic evaluation of the current or competitor
product (Nielsen's heuristics, severity-rated). Synthesize into personas (only
when evidence supports them), journey maps, and opportunities. We state sample size and
confidence honestly and never invent quotes or numbers.

**Information architecture.** Content inventory and audit (critical in redesigns),
sitemap and navigation model, and the object model the UI must represent.

**User flows.** Map the happy path plus edge cases, empty, loading, error,
permission-denied, offline, first-run, and success states, with decision points
and data sources noted.

**Wireframes.** Establish layout, hierarchy, and interaction logic without visual
styling, and validate structure before high fidelity.

**High-fidelity UI.** Apply the design system and tokens with real content. Design
every state (default, hover, focus, active, disabled, loading, empty, error,
success, overflow) and define responsive behavior across breakpoints. Flows and
screens can iterate as v1, v2, v3, we keep a version history (Figma
branching/version history and a changelog), and when we explore alternatives we
state the hypothesis and the single change each variant tests.

**Prototyping.** Build clickable prototypes at the fidelity the decision requires,
focusing on the interactions and transitions that carry meaning. When useful, the
designer produces a **coded front-end prototype** in the chosen framework, wired
to the brand tokens, a runnable base that gives engineering a concrete starting
point. It's clearly labeled prototype-grade (real vs mocked), distinct from the
production implementation delivered at handoff. Dynamic data lives in a separate
layer, JSON fixtures behind a single typed data-access module (optionally a
mock network via MSW/json-server), shaped to the real API contract, so the UI
is decoupled from data and swapping to live endpoints is mechanical. When we need
to compare alternatives, we build variants (v1, v2) behind branches or feature
flags, sharing the same data layer and instrumented so they can be measured, the
basis for A/B testing, decided in validation against the DoR success metric. To
make the prototype a real base for development rather than a throwaway, we build
it inside engineering's conventions when they exist (a dev-provided scaffolding
skill, repo structure, component library, data-fetching pattern) and reuse their
components; when they don't, we hand over a short contract documenting the choices
so engineering can adopt or extend it.

**Usability testing.** Define tasks and success criteria, test with representative
users, log findings by severity, and re-test fixes.

---

## 4. Our checkpoints: Definition of Ready and Definition of Done

Every design task has a checkpoint at both ends.

### Definition of Ready: before we design

A task is Ready only when we can answer all of the following. If a core item is
missing, we gather it, draft it as a labeled hypothesis, or escalate, we don't
start on a missing core item.

1. Problem & goal, the user problem and business outcome it serves.
2. Users & context, who, on what device, at what moment in the journey.
3. Scope, what's explicitly in and out.
4. Success criteria, how we'll know it worked.
5. Constraints, platform, framework, existing components, data, performance,
   legal/compliance, brand.
6. Inputs available, research, analytics, prior designs, content, decisions.
7. Dependencies, what must exist first and who owns it.
8. Accessibility & localization, WCAG target, RTL, languages, dynamic type.

### Definition of Done: before handoff

The task is Done only when all of these hold:

1. Solves the stated problem and meets the success criteria.
2. All relevant states and responsive breakpoints are designed.
3. Built from the design system / tokens, or deviations documented as exceptions.
4. Meets WCAG 2.2 AA, verified, not assumed.
5. Motion and transitions specified where they carry meaning.
6. Documentation and rationale complete.
7. Content and copy finalized (no placeholders).
8. Developer handoff ready, tokens and components map to the framework, assets
   exported, specs unambiguous.
9. Design QA passed and reviewed with engineering/PM.
10. Open questions, assumptions, and risks listed.

---

## 5. Design system

We treat the design system as a product with its own lifecycle: foundations →
primitives → patterns. What we do depends on the mode (create, audit/extend, or
consume).

**Tokens start from the brand and are the source of truth.** The brand, its
palette, typefaces, shape language, and motion personality, becomes the
primitive token layer; from there we define semantic/alias tokens (meaning-based,
e.g. `color.action.primary`) → component tokens. Tokens are never chosen
arbitrarily and "styled to brand" later. Themes (light/dark, and multiple
brands / white-label) flow through the semantic layer, so a brand swaps at the
token level without touching components. Tokens map to the framework's theme
config, never a hardcoded value that a token should own. We verify brand colors
meet contrast targets and resolve conflicts at the semantic layer rather than
abandoning the brand.

**Components** are specified with anatomy, variants, states, props/API, do's and
don'ts, and accessibility behavior, named to mirror the framework's real API so
translation to code is mechanical.

**Governance** covers how a new component gets proposed, reviewed, and added. Every
change carries rationale, affected surfaces, and a migration note. When we consume
an existing system, any deviation is a documented, routed exception, never silent
divergence.

Where the team uses **Storybook**, it is a first-class deliverable of the design
system, the living component library. Each component ships with a story covering
its variants, states, props/controls, and accessibility, bound to the same tokens
as the app and kept in sync with the design source. Storybook becomes the shared
reference between design and engineering and a primary surface for design QA.

---

## 6. Motion & transitions

Motion communicates; it is not decoration. Every animation must do a job: orient,
give feedback, show relationships, express hierarchy, or indicate progress. If it
has no job, we cut it.

We define duration and easing tokens (fast ~100-150ms for micro-feedback, base
~200-300ms for most transitions, slow ~400ms+ for large changes) and reuse them
like color tokens. We specify motion precisely for engineering (trigger,
properties, from/to, duration, easing, delay, interrupt behavior), prefer
GPU-friendly properties (transform, opacity), and always honor
`prefers-reduced-motion` with a reduced or no-motion fallback. We never rely on
motion alone to convey information.

---

## 7. Documentation

Documentation is a first-class deliverable. We produce the right doc for the
audience: design rationale / decision records (problem, options, decision, why);
flow and screen annotations (behavior, states, validation, edge cases, data
sources); component docs (anatomy, variants, props, usage, accessibility); content
and copy (microcopy, empty states, error messages); and a changelog for redesigns
and system updates. Docs are versioned and kept close to the design source, with a
single source of truth over scattered notes.

---

## 8. Design QA

We run structured QA in two passes.

**Pre-handoff (design vs. intent):** all states designed; responsive behavior
defined; tokens and components used correctly with no rogue values; accessibility
checked (contrast, focus order, visible focus, target sizes, labels, keyboard,
error identification); real content, not lorem ipsum; motion specified with a
reduced-motion fallback.

**Post-implementation (build vs. design):** visual parity against tokens;
interaction and motion match spec; state and responsive coverage verified in the
real build; accessibility verified with keyboard and a screen reader; no
regressions.

Findings are logged by severity, blocker, major, minor, polish, each tied to a
specific screen or component so it's fixable without a meeting.

---

## 9. Accessibility

WCAG 2.2 AA is our baseline. We check the four principles, perceivable (text
alternatives, 4.5:1 / 3:1 contrast, reflow, not relying on color alone), operable
(keyboard, visible and unobscured focus, ≥24×24px targets, no traps), 
understandable (clear labels, error handling, consistent navigation), and robust
(semantic markup, correct roles/states, announced status). We honor reduced
motion, and for regulated projects we raise whether a higher bar (AAA or a legal
standard such as ADA, Section 508, EN 301 549) applies. We verify with real
assistive technology, not automated tools alone.

---

## 10. Developer handoff

Handoff targets Figma plus the project's existing front-end framework. We deliver
an organized Figma file (named layers, published components/variants, tokens as
variables/styles), a concrete token → theme mapping (CSS variables, Tailwind
config, MUI theme), a component → code mapping to the library's real API so
translation is mechanical, annotated specs (states, responsive rules, motion,
edge cases), and exported assets at correct densities. We offer a short handoff
walkthrough so engineering can raise feasibility concerns before building.

---

## 11. How we collaborate

Design fits into the team's sprint cadence rather than working in isolation. In
**backlog refinement** we pressure-test stories against the DoR and flag missing
inputs early. In **sprint planning** we size design work realistically and call
out research or content dependencies. We run regular **design critiques** that
separate "does it meet goals" from personal preference. **Three amigos**
(design + dev + PM/QA) align on acceptance criteria and edge cases before build.
In **demos and retros** we show outcomes against success criteria and feed
learnings back into the system and docs.

---

## 12. The tooling: agent + skills

This practice is encoded in a Cowork toolkit the whole team can use:

- **Prisma (UX/UI Design Agent)**, the expert design partner that applies
  everything in this playbook end to end, across all three project modes.
- **design-dor-dod**, generates and validates the Ready and Done checkpoints for a task.
- **frontend-stack-advisor**, recommends the front-end framework/library by
  platform and project type, decided in discovery.
- **ia-user-flows**, defines information architecture and user flows covering
  every state; its state inventory feeds the prototype and design QA.
- **design-system**, creates, audits, extends, or consumes a design system.
- **frontend-prototype**, generates a coded front-end prototype as a dev-ready base.
- **figma-to-frontend**, converts a finalized Figma design into production code.
- **design-qa**, runs the two-pass quality review with a severity-ranked log.
- **heuristic-evaluation**, audits usability against Nielsen's heuristics with
  severity ratings; used in research and as expert review.
- **accessibility-audit**, runs a WCAG 2.2 AA audit with prioritized fixes.

Prisma is the "brain" for judgment across a whole engagement; the skills are the
repeatable procedures you invoke for a specific task. Use Prisma when you need
design thinking; reach for a skill when you need a specific checkpoint, audit, or
conversion done consistently.

---

## 13. Quick reference

**Starting a task?** Run the DoR. If a core item is missing, don't design yet, unblock it first.

**Finishing a task?** Run the DoD and a design QA pass before handoff.

**Adding a UI pattern?** Check the design system first. Reuse, then extend, then
(only if necessary) propose a new component through governance.

**Handing off?** Map tokens and components to the framework, annotate states and
motion, export assets, and walk engineering through it.

**Unsure about accessibility?** Run the accessibility audit, AA is the floor,
and regulated work may need more.
