---
name: frontend-prototype
description: >
  Generate a working, coded front-end prototype from the design to serve as a
  dev-ready base for the engineering team. Use when a designer needs a runnable
  prototype (not just a clickable mockup), triggers like "build a front-end
  prototype", "make a coded prototype", "prototype this flow in React/shadcn",
  "create a coded base for developers", or "turn this flow into a working
  prototype". Uses the project's chosen framework and design tokens, covers the
  key flows and states, and is clearly labeled prototype-grade vs production.
---

# Front-end Prototype

Produce a runnable, coded prototype that validates flows and interactions and
gives engineering a concrete base to build on. This is earlier and lighter than
production implementation, its value is speed, realism, and a shared reference,
not final code.

## When to use
After user flows / wireframes (or high-fidelity) and after the framework is
decided. Use it to validate interactions, pressure-test the design in a real
browser/device, and hand engineering something they can run and extend.

## Prerequisites
- Framework/library decided (see `frontend-stack-advisor`).
- Design tokens available and mapped to the framework theme (see `design-system`).
- The flows/screens and their states from the design.
- **Check for engineering's conventions or a dev-provided skill** (see below)
  before scaffolding, adopting them from the start is what makes the prototype
  reusable rather than throwaway.

## Make it reusable: align with engineering
The prototype is most valuable when it can become the base for development, not a
parallel artifact engineering has to rebuild. So this skill is designed to work
**in conjunction with an engineering-provided skill or convention set** when one
exists.

- **Detect and defer.** At setup, look for the dev team's scaffolding skill,
  starter/boilerplate, or conventions doc. If present, defer to it for: repo and
  folder structure, framework/version, component library, state management,
  data-fetching pattern, styling/token wiring, linting/formatting, testing setup,
  env/config, and commit/PR conventions. Build the prototype *inside* those
  conventions so it can be adopted directly.
- **Reuse their components.** Prefer the engineering team's existing component
  library / design-system package over re-implementing; the prototype should
  consume the same components production will.
- **Align the seams.** Match their data-fetching approach so the data layer
  (fixtures/MSW) plugs into the real one by swapping endpoints, and their
  token/theme wiring so styling carries over.
- **When no dev skill/convention exists yet:** build in a clean, conventional
  structure and emit a short **handoff contract** documenting the choices
  (framework + version, folder structure, dependencies, token source, data
  contract, component mapping, env/config, and what is prototype-grade vs
  production). Recommend the dev team capture these as a shared engineering skill
  so future prototypes are reusable by default. Treat this contract as the
  agreement that lets engineering adopt or extend the prototype.
- **Co-own the boundary.** Agree with engineering, up front, on what the
  prototype will and won't include and how it will be handed over, so
  expectations about "reusable base" are shared, not assumed.

## Steps
1. **Scope it.** Pick the key flows/screens and the fidelity the decision needs.
   Prefer thin vertical slices over covering everything. State what you're
   validating.
2. **Set up with the chosen stack + tokens.** Reuse the design system / library
   components; wire the theme to the brand tokens so the prototype looks on-brand,
   not default.
3. **Build the flows** with realistic content and the meaningful states (loading,
   empty, error, success), the interactions and motion that carry meaning, and
   responsive behavior across the target breakpoints/devices.
4. **Cover accessibility basics** even in a prototype: semantic markup, keyboard
   operability, visible focus, labels.
5. **Label reality.** Clearly mark what is real vs mocked (data, auth, backend),
   what is prototype-grade and must be hardened for production, and known gaps.
   This is a base/reference, not a finished feature.

## Data layer: keep data separate from UI
Never hardcode dynamic data inside components. Model it as its own layer so the
prototype behaves like the real app and the swap to production is mechanical.

- **Fixtures in a dedicated location:** keep mock data as JSON (or TS modules) in
  a `/data` (or `/mocks`) folder, one file per entity/resource. Components never
  import these directly.
- **Access through one seam:** read data through a single typed module, a
  `dataProvider` / repository / service (e.g. `getUsers()`, `getOrder(id)`). It
  reads fixtures today; later you point that one module at the real API without
  touching any component.
- **Match the real contract:** shape the JSON to the agreed API contract and
  types (TypeScript types or JSON Schema, aligned with backend) so field names
  and structure map 1:1 to production.
- **Model reality, not the happy path only:** include empty results, long lists,
  long strings, nulls/optionals, and error payloads so the UI's loading, empty,
  and error states are actually exercised.
- **Simulate the network when realism matters (preferred):** use **MSW (Mock
  Service Worker)** or `json-server` so the prototype makes real `fetch`/HTTP
  calls that are intercepted and answered from fixtures, with simulated latency
  and error responses. The data-fetching code then carries straight into
  production; only the endpoint changes.
- **Document the contract:** in the README, note each resource, its shape, what
  is mocked vs real, and how to switch to live endpoints.

## Output
A runnable prototype (repo or project with run instructions), the `/data`
fixtures and the data-access module (plus MSW/json-server handlers if used), and
a short README covering scope, flows included, mocked vs real data, the data
contract, and known gaps, plus a brief handoff note for engineering. Keep the
code readable and close to the project's conventions so it can be extended
rather than thrown away where that makes sense.

## Variants & A/B testing
A prototype often needs to compare alternatives (v1, v2, v3) before committing.
- **Isolate each variant** as a git branch/tag or behind a **feature flag /
  variant switch**, so you can serve different versions without forking the whole
  prototype.
- **Share the data layer** across variants so only the difference under test
  varies, same fixtures/contract, different UI or flow.
- **Instrument the meaningful events** (clicks, completions, drop-off) so each
  variant is measurable; keep the analytics seam mockable like the data layer.
- **Document each variant** with its hypothesis, what differs, and the success
  metric it targets. After the test, converge on the winner and retire the rest,
  keeping the version history.
- Keep the versioning convention explicit (naming, changelog) so design,
  prototype, and, later, production stay aligned on which version is which.

## Template
Use the bundled `templates/version-ab-log.csv` to track variants (v1/v2/v3), each
with its hypothesis, the single change under test, the success metric, result, and
decision.

## Distinction from `figma-to-frontend`
- **frontend-prototype:** earlier, exploratory/validation, may cut corners,
  explicitly labeled as a base, optimized for speed and coverage of key flows.
- **figma-to-frontend:** production implementation of finalized designs, full
  fidelity to tokens/components, no rogue values, ready to ship.

## Notes
- Don't gold-plate a prototype; its job is to answer questions and de-risk build.
- Pair with `design-qa` to review the prototype's states and interactions, and
  with `frontend-stack-advisor` if the prototype reveals the stack is a poor fit.
