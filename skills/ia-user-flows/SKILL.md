---
name: ia-user-flows
description: >
  Define the information architecture and user flows for a product or feature, content inventory, sitemap, navigation model, object/entity model, and
  end-to-end flows that cover every state. Use in the Structure phase, after
  intake and before wireframes, triggers like "map the user flow",
  "create a sitemap", "information architecture", "define the navigation", "what
  states does this flow need?", "flow for this feature", or "manage the use
  cases / happy and sad paths". Its object model feeds the prototype's data
  contract and the design contract, and its per-flow state inventory becomes the
  checklist design-qa verifies against.
---

# Information Architecture & User Flows

Give the product its structure and define how people move through it. This is the
Structure phase: it turns intake into the skeleton that wireframes,
the design contract, the prototype, and QA all depend on. Its main risk is missing
states and edge cases, so completeness is the point.

This skill carries the most weight on **intake Path B** (requirements only):
nothing upstream has defined the sad paths yet, and if this skill doesn't
name them, no one will until a build agent has to invent one. On Path A,
some of this may already exist in the live product, extracted by
`figma-intake`, use this skill to fill the gaps that extraction reports.

## When to use
After intake, before wireframes. Adapt depth to the intake path: Path A
emphasizes the content audit and old→new mapping; Path B emphasizes the
object model and flows.

## Part A: Information architecture
- **Content inventory & audit** (essential for redesigns): list existing
  content/features with owner and a keep / cut / merge / revise decision.
- **Sitemap & navigation model:** page/section hierarchy, primary and secondary
  navigation, entry points, and cross-links.
- **Object / entity model:** the key entities, their attributes, relationships,
  and lifecycle states. This doubles as the basis for the API shape and the
  prototype's **data contract** (see `frontend-prototype`) and maps entities to
  components (see `design-system`).
- **Validate contested structure** with card sorting or tree testing rather than
  guessing.

## Part B: User flows & use cases
Model each key task as a **use case** with its paths, this is where happy paths
and sad paths are managed (there is no separate skill for it; it lives here and
is verified in `design-qa`):
- **Happy path:** the main successful route through the task.
- **Sad / alternate paths:** everything that deviates, invalid input, failed
  validation, errors, timeouts, no results, no permission, offline, cancellation,
  back/undo, and recovery. Every sad path needs a defined UI response, not just
  the happy one.
- One flow per use case. For each, show the trigger, the steps, decision points,
  system responses, and the **data source** at each screen.
- **Cover every state explicitly**, this is the part most often missed and the
  usual source of downstream rework:
  happy path · empty · loading · error · permission-denied / unauthorized ·
  offline / no-connectivity · first-run / onboarding · success / confirmation ·
  edge & overflow (zero / one / many, long lists, long strings).
- Note validation rules and error messages at each decision point.
- Keep flows tool-agnostic and reviewable before committing to wireframes.

## Output
A content inventory (for redesigns), a sitemap / navigation model, an
object/entity model, and a set of user-flow specs, each with an explicit
**per-flow / per-screen state inventory**. Deliver the state inventory in a form
the team can check off, because it is reused downstream.

## Versioning & flow variants
A flow can iterate, v1, v2, v3, and can branch into alternatives to compare.
- Keep a **version history / changelog** for flows and their state inventories so
  changes are traceable (what changed, why, when).
- When proposing alternatives for A/B testing, define the **hypothesis** and the
  single meaningful difference each variant introduces, plus the success metric
  it targets (tie it to the DoR success criteria). Keep variants minimal, one
  deliberate change, so results are attributable.
- The winning variant becomes the canonical flow; retire the rest but keep the
  record. Variants defined here are built in `frontend-prototype` and measured in
  usability/validation.

## Template
Use the bundled `templates/flow-state-inventory.csv` to record each use case, its
happy and sad paths, states, data sources, and the designed/built check columns.
It is the artifact `design-qa` verifies against.

## How it connects
- **design-system:** entities → components; entity/flow states → component states.
- **frontend-prototype:** the object/entity model becomes the data contract and
  the shape of the JSON fixtures.
- **design-qa:** the per-flow/per-screen state inventory *is* the checklist QA
  verifies against, every state defined here must be designed and built. Define
  completeness once here; enforce it later in QA.

## Notes
- Don't skip edge/error/empty states; they are cheap to plan now and expensive to
  discover in build.
- Pair with `design-dor-dod`: a Ready task should already name its users, scope,
  and data; a Done flow should have every state covered.
