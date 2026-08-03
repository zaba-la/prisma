---
name: figma-intake
description: >
  Intake path A: extract the design contract from an existing Figma file or
  a live product, reconciled against whichever one actually reflects the
  current product. Use when a client already has a design or a running
  product, triggers like "we already have a Figma file", "pull the tokens
  out of this Figma", "audit this design system from Figma", "this app
  exists, no Figma", or "extract the design contract from the live
  product". Reports state, responsive, and motion coverage gaps rather than
  assuming the file is complete. Produces the design contract, never
  production code, build agents implement downstream.
---

# Figma Intake (Path A)

Turn an existing Figma file, a live product, or both, into the design
contract other agents build against. The file or the running app is a
source, never the contract itself: it drifts, it's usually silent on states
and motion, and the goal here is to pull out what's real and name what's
missing, not to hand it forward as-is.

## Prerequisite: use the Figma tooling correctly
If the Figma MCP/plugin is connected, the `figma:figma-design-to-code`
skill is the MANDATORY prerequisite before calling `get_design_context`;
load it first. This skill layers the design-contract extraction and
coverage-reporting rules on top of that flow. If Figma access is not
authorized, work from exported specs/screenshots the user provides, or from
the live running product, and note that live Figma access would tighten
fidelity.

## Step 1: Establish which reference wins
When both a Figma file and a live product exist, they will have drifted.
Decide explicitly which one is the source of truth for this extraction
(usually the live product for anything already shipped, the file for
anything not yet built) and record that decision, later QA diffs depend on
knowing which reference was authoritative.

## Step 2: Extract into the design contract
- **Tokens:** pull Figma variables/styles (or computed styles from the live
  product) into real tokens, color, type scale, spacing, radius, elevation,
  motion. Do not leave a hardcoded value where a token should exist.
- **Components:** map each Figma component/variant (or live UI pattern) to
  its anatomy, variants, states, and props. Add a Code Connect map where
  components already exist in code, so the mapping from design to
  implementation is mechanical downstream.
- **Motion and interaction:** note what's actually specified versus implied;
  most client files specify almost none of this.

## Step 3: Reconcile
Compare the extracted contract against whichever reference won in Step 1.
Flag every discrepancy: a token in the file that no longer matches the live
product, a component variant that exists in code but not in the file, or the
reverse. Don't silently prefer one over the other, name the conflict and
resolve it in the design contract with a rationale.

## Step 4: Report coverage
Most client files are silent on:
- Empty, error, and loading states.
- Responsive behavior across breakpoints.
- Motion and transition specs.

Report these gaps explicitly rather than treating extraction as complete.
Closing them is real design work, hand it to the normal lifecycle (see
`agents/prisma.md` §3), not something this skill can pull out of a file
that never specified it.

## Output
The design contract (tokens with framework mapping, component specs, the
Code Connect map where it applies), a reconciliation note naming which
reference won and any conflicts resolved, and a coverage report listing
what states, responsive rules, and motion specs are still missing and need
real design work. This skill does not produce production code, that
implementation is a build agent's job once the design contract and
prototype (`frontend-prototype`) exist.

## How it connects
- Feeds `design-system`, which owns the design contract this skill
  populates.
- Feeds `frontend-prototype`, which builds the contract into a runnable
  prototype.
- Coverage gaps found here become work items in the normal lifecycle
  (`ia-user-flows` for missing states, `design-system` for missing tokens).
