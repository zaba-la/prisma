# UX/UI Design Playbook

A shared handbook for how we do product design. It exists so that
designers, engineers, and product managers work from the same definitions,
rituals, and quality bar, whether we're building a product from zero, redesigning
a legacy one, or contributing to an established design system.

This playbook is the human-readable companion to **Prisma**, our UX/UI Design
Agent, and its skills. Prisma applies these same standards inside Cowork; this
document is what the team reads, references in tickets, and uses to onboard new
members.

Prisma is one stage in a multi-agent build pipeline, not a solitary designer.
It takes requirements in, produces a design contract, a prototype, and a
build brief, and proves whether a build matches them. It does not run
discovery and it does not write production code, both happen elsewhere in
the pipeline. This playbook reflects that division of labor throughout.

---

## 1. What we believe

Design here is accountable for outcomes, not just screens. A few
principles guide every engagement:

**Contract and proof, not build.** Prisma's output is a design contract, a
prototype, and a build brief. Build agents write production code elsewhere
in the pipeline. Prisma's QA proves whether their output matches the
contract, it does not gatekeep their work.

**Advise, never block.** Findings travel as severity-tagged recommendations.
A violation that survives a recommendation escalates to a human, it does not
stop the pipeline. Because we cannot stop bad output after the fact, our
real lever is making the contract complete enough that a build agent does
not produce the bad output in the first place.

**Runs without a human present.** The design contract, the prototype, the
build brief, and the QA report are the real interface between agents.
Natural language sits on top of that for humans, but no step should require
a human to be there to answer a question. Where the process would stop and
ask, it defaults to a labeled assumption instead.

**Requirements in, no discovery.** Primary research happens upstream, before
Prisma is invoked. We do define what a requirements handoff must contain
(the intake spec), and we're allowed to call a handoff incomplete only under
a narrow blocking rule.

**Outcomes over deliverables.** Every artifact traces back to a job to be
done and a business goal named at intake. If we can't state the "why," we
record it as an assumption and keep moving rather than stopping to ask.

**Evidence before opinion.** We prefer intake data and heuristics over
taste. When we rely on taste, we say so, and route it through the design
contract.

**Constraints are inputs, not blockers.** Platform, tech stack, timeline, team
maturity, and accessibility requirements shape the design from the start.

**Brand is the foundation, not the veneer.** The design contract starts from the
brand, its identity, personality, and voice. Tokens encode the brand rather than
being chosen arbitrarily and styled later.

**Systematize by default.** We reuse before we create. A new pattern either fits
the design contract or is proposed as a contract change, never a silent one-off.

**Accessibility is not optional.** WCAG 2.2 AA is our baseline on every project.
Regulated work (healthcare, finance, public sector) may require more, and we raise
that early.

**Small, reviewable increments.** We state how many review rounds are
included before we start, and ship in thin vertical slices rather than a
big-bang reveal.

---

## 2. Intake: two paths, one merge point

Before any design work, we decide which intake path applies and which
operating mode the project runs in. Neither is inferred in silence.

**Path A: an existing Figma file or live product.** The file (or the running
product) is a source, never the contract. We extract variables, styles, and
components into real tokens, add a Code Connect map where components exist
in code, and reconcile against the live product, files drift, and the QA
diff later depends on knowing which reference wins. We report coverage
explicitly: client files are almost always silent on empty, error, and
loading states, on responsive behavior, and on motion, and closing those
gaps is real design work.

**Path B: requirements only.** Nothing is pre-decided, so the system comes
before the screens: we settle the front-end stack and author a token set
before any screen exists. Information architecture and user flows do their
most important work here, especially the sad paths, since nothing upstream
has defined them yet.

Both paths converge on the same three artifacts, the only interface between
agents:

1. **Design contract**, tokens, type scale, spacing, color roles, motion
   rules, who it's for and how it should feel, plus the assumption register
   from intake.
2. **Prototype**, the core experience built in the real system with
   realistic data. What a build is judged against.
3. **Build brief**, scope edges, acceptance checks a build agent can run on
   itself, and the edge states deliberately left open.

For every project we also confirm the platform(s), the front-end framework in
play (e.g. React + shadcn/ui, Tailwind, MUI, SwiftUI), and, on Path A, the
design tool (Figma by default).

---

## 3. The design lifecycle

We adapt depth to the intake path and operating mode, but we never skip a
phase silently, if we compress or drop one, we say why in the design
contract.

**Intake & framing.** Run the DoR intake against the intake spec (section 4)
and record the verdict and assumption register. Decide the intake path and
confirm the operating mode with whoever owns the scope of work. **Capture
the brand foundation** if it exists, or record the minimal assumed
direction if it doesn't. **Decide the front-end stack** on Path B, based on
platform and project type, and record it with rationale in the design
contract.

**Research, only when it's already upstream.** We don't run primary
research. If interviews, surveys, or analytics already exist upstream, we
fold their findings into intake. Expert review of what already exists stays
fair game before designing, heuristic evaluation of the current product or a
competitor surfaces problems without new user contact. We never invent
quotes, numbers, or personas.

**Information architecture.** Content inventory and audit (critical on Path
A), sitemap and navigation model, and the object model the UI must
represent, this becomes the prototype's data contract.

**User flows.** Map the happy path plus edge cases, empty, loading, error,
permission-denied, offline, first-run, and success states, with decision
points and data sources noted.

**Wireframes.** Establish layout, hierarchy, and interaction logic without
visual styling. In client-in-the-loop mode we skip wireframes as a client
deliverable unless asked, and render concepts in the real system instead.

**High-fidelity UI.** Apply the design contract's tokens with real content.
Design every state (default, hover, focus, active, disabled, loading, empty,
error, success, overflow) and define responsive behavior across breakpoints.
Flows and screens can iterate as v1, v2, v3, we keep a version history and a
changelog in the design contract.

**Prototyping: the contract, plus the build brief.** The prototype is not a
base or a reference, it is **the contract**. A build is judged against the
approved prototype, not a written spec. We build it runnable, wired to the
design contract's tokens, covering the key flows and their states. Alongside
it, we produce the **build brief**: scope edges, acceptance checks a build
agent can run on itself, and edge states we're deliberately leaving open.
Dynamic data lives in a separate layer, JSON fixtures behind a single typed
data-access module, shaped to the real API contract, so the UI is decoupled
from data. In client-in-the-loop mode we produce one concept by default
(section 11), rendered in the real system, never a wireframe unless asked.
We do not write the production implementation, that's a build agent's job
downstream.

**Usability testing.** Define tasks and success criteria from intake's
success signal, test with representative users when that testing already
exists in the pipeline, log findings by severity, and route each one through
the layered QA model (section 8).

---

## 4. Our checkpoints: the intake spec, and Definition of Ready / Done

Every design task has a checkpoint at both ends. These are **decision
gates**, few, named, and each paired with a rendered artifact, not the
dozens of automatic **quality gates** that run underneath them (section 8).

### The intake spec

A functional spec tells engineers what to build. It rarely tells a designer
what to design. We publish an intake spec as its own deliverable, asking
for: jobs to be done (without reference to software), how people do it
today, users in the plural with context of use, user stories with the "so
that" clause intact, realistic data (including the ugly cases: the
60-character name, the empty list, the 10,000-row table), and the scope
edges. Useful and cheap to add: known failure modes, hard constraints
(stack, devices, accessibility, localization, brand), and how we'll know it
worked.

Intake returns one of three verdicts. **Complete**, go. **Complete with
assumptions**, the normal case, we fill the gap, write it into a numbered
assumption register, and keep moving. **Blocked**, only for three reasons:
no realistic data, no users, no jobs to be done. We default to assuming, not
to a clarification round back to whoever sent the requirements, a
questionnaire reads as the system not working.

### Definition of Ready: before we design
A task is Ready only when intake against the spec above returns Complete or
Complete with assumptions, with every assumption recorded.

### Definition of Done: before handoff

The task is Done only when all of these hold:

1. Solves the stated jobs to be done and meets intake's success signal.
2. All relevant states and responsive breakpoints are designed.
3. Built from the design contract, or deviations documented as exceptions.
4. Meets WCAG 2.2 AA, verified, not assumed.
5. Motion and transitions specified where they carry meaning.
6. The build brief's acceptance checks pass, and a visual diff against the
   prototype is attached, not just described.
7. The feel verdict has run (the client's concept review, or Prisma's own
   fresh-context pass in lights-out mode).
8. Documentation and the design contract's rationale are complete.
9. Content and copy finalized (no placeholders).
10. Open questions, assumptions, and risks listed in the assumption
    register.

---

## 5. Design contract

We treat the design contract as the single, hand-maintained source of truth
for one project, not a box labeled "design system." It has a schema:
tokens (color, type scale, spacing, radius, elevation, motion), semantic
color roles named by meaning, motion rules, who the product is for and how
it should feel stated concretely enough to check output against, the
assumption register carried forward from intake, and component specs
(anatomy, variants, states, props/API, accessibility behavior) named to
mirror the front-end framework's real API.

**Tokens start from the brand.** The brand, its palette, typefaces, shape
language, and motion personality, becomes the primitive token layer; from
there we define semantic/alias tokens (meaning-based, e.g.
`color.action.primary`) then component tokens. Themes flow through the
semantic layer, so a brand swaps at the token level without touching
components. We verify brand colors meet contrast targets and resolve
conflicts at the semantic layer rather than abandoning the brand.

**Platform-level vs project-level.** The process that produces a design
contract, the skills, the craft floor, installs once for the whole practice.
Each project carries only its own design contract, a single hand-maintained
file, never a generated snapshot edited by hand.

**Governance** covers how a new component gets proposed, reviewed, and
added. Every change carries rationale, affected surfaces, and a migration
note. On Path A, any deviation from the client's existing system is a
documented, routed exception, never silent divergence.

Where the team uses **Storybook**, it is a first-class deliverable, the
living component library, bound to the same tokens as the app and kept in
sync with the design contract.

---

## 6. Motion & transitions

Motion communicates; it is not decoration. Every animation must do a job:
orient, give feedback, show relationships, express hierarchy, or indicate
progress. If it has no job, we cut it.

We define duration and easing tokens (fast ~100-150ms for micro-feedback,
base ~200-300ms for most transitions, slow ~400ms+ for large changes) in the
design contract. We specify motion precisely for build agents (trigger,
properties, from/to, duration, easing, delay, interrupt behavior), prefer
GPU-friendly properties (transform, opacity), and always honor
`prefers-reduced-motion` with a reduced or no-motion fallback. We never rely
on motion alone to convey information.

Motion is the one dimension a deterministic script can't check, so we lean on
vendored skills for the mechanics instead of building equivalents:
`find-animation-opportunities` to spot where motion is warranted,
`improve-animations` to audit and plan fixes, `review-animations` against its
craft bar, `animation-vocabulary` to name an effect precisely, and
`apple-design` for spring-based, interruptible motion physics. Each carries a
house rule, they own the mechanics, our design contract's stated motion
personality always wins on an aesthetic call.

---

## 7. Documentation

Documentation is a first-class deliverable. We produce the right doc for the
audience: design rationale / decision records folded into the design
contract; flow and screen annotations (behavior, states, validation, edge
cases, data sources); component docs (anatomy, variants, props, usage,
accessibility); content and copy (microcopy, empty states, error messages);
and a changelog kept inside the design contract. Docs are versioned and kept
close to the contract, a single source of truth over scattered notes.

---

## 8. Design QA: advisory, layered by cost

QA never blocks a build agent. It proves whether a build matches the
contract and returns severity-tagged recommendations. A violation that
survives a recommendation escalates to a human, it never stops the
pipeline.

**Two kinds of checkpoint, kept separate.** Quality gates run on the
machine: automatic, invisible, and there can be dozens. Decision gates are
where a human commits to something: few, named, always paired with a
rendered artifact. How many decision gates a project has falls out of the
operating mode (section 11): zero in lights out, one in client in the loop.

**Three layers, cheapest first.** Creation-time context (the contract and
build brief are complete enough that a build agent builds correctly the
first time); a deterministic detector (a plain script, no model, checking
output against the craft floor on every UI file edit, non-blocking); and
judgment critique last, against the design contract and the craft floor's
hard rules. Accessibility belongs primarily in the first two layers, by the
time it reaches judgment critique it's remediation, not prevention.

**Fresh context, always.** Whoever runs judgment critique does it with no
visibility into the conversation that produced the design, briefed only by
the artifact. A critic that shares context with the work it's checking
optimizes for agreeing with itself.

**Pre-handoff (design vs. intent):** all states designed; responsive
behavior defined; contract fidelity (tokens and components used correctly,
no rogue values); accessibility checked; real content, not lorem ipsum;
motion specified with a reduced-motion fallback.

**Post-implementation (build vs. prototype):** a visual diff, not a
sentence, screenshots of the prototype and the build at matching viewports,
diffed and attached. Interaction and motion match spec; state and responsive
coverage verified in the real build; accessibility verified with keyboard
and a screen reader; no regressions.

**The feel verdict.** Functional QA proves it works and matches, it can't
judge taste. That needs its own gate: the client's concept review in
client-in-the-loop mode, or Prisma's own fresh-context pass before delivery
in lights-out mode. We don't ship on functional parity alone.

Findings are logged by severity, blocker, major, minor, polish, each tied to
a specific screen or component so it's actionable without a meeting.

---

## 9. Accessibility

WCAG 2.2 AA is our baseline. We check the four principles, perceivable (text
alternatives, 4.5:1 / 3:1 contrast, reflow, not relying on color alone), operable
(keyboard, visible and unobscured focus, ≥24×24px targets, no traps), 
understandable (clear labels, error handling, consistent navigation), and robust
(semantic markup, correct roles/states, announced status). We honor reduced
motion, and for regulated projects we raise whether a higher bar (AAA or a legal
standard such as ADA, Section 508, EN 301 549) applies. Most of this runs in
the early, cheap layers of QA (section 8), not as a phase-5 discovery. We
verify with real assistive technology, not automated tools alone.

---

## 10. Build brief: handoff to build agents

Our handoff is narrower than "engineering builds this from a Figma file." We
produce two deliverables and one check; build agents elsewhere in the
pipeline do the implementation. We deliver the design contract (tokens as
variables/styles, component specs, the assumption register), the prototype
(the runnable reference a build is judged against), the build brief (scope
edges, self-checkable acceptance checks, deliberately open edge states,
written so a build agent can verify them without asking us), and a concrete
token/component mapping to the framework's real API. Once a build exists, we
run the post-implementation QA pass and attach the visual diff, that's our
proof, not a blocker.

---

## 11. Two operating modes

We confirm the mode at intake. It's a commercial decision that belongs in
the scope-of-work conversation, never a silent default, and it can be mixed
by surface within one project (a first-impression screen gets a concept
review, an internal CRUD screen runs lights out).

**Lights out.** The client sees only the finished product. Zero human design
gates. Design risk lands at the end, a wrong direction costs a full cycle.
It buys speed and costs rework risk. Feedback returns mixed (design,
product, defects, new requirements) and we route it with a triage step:
every item goes to a design contract change, a prototype change, a build
defect, or a new requirement. Skipping triage is what makes this mode drown
in its own feedback. We run the feel verdict ourselves before delivery,
since there's no client gate to catch a functionally correct but off-brand
result.

**Client in the loop.** The client sees the concept, then the product. One
human gate: the concept review. **One concept by default**, not several,
requirements already answered "what to build," the remaining question is
"is this right," and one concept answers that better than three (three
triples a scarce billed review round and invites assembling a favorite
header with a favorite table, that's editing by committee, not feedback).
Exceptions: brand-defining surfaces, a genuinely novel interaction with no
precedent, or the client asks. We render in the real system with realistic
data, never wireframes unless asked, and state plainly what the concept
commits to and what's still open. Feedback returns as a design contract
change, never a live edit. One batched review round by default, and we
state how many rounds are included from the start, rounds are what erode
margin. Feel-words ("heavy," "feels enterprise") are valid feedback,
translating them into concrete contract changes is our job, proposed back
for a yes.

**What holds regardless of mode.** The machine layers (design contract
through build brief) are identical in both modes, client review sits on top
of the craft floor, it never replaces it.

---

## 12. Craft floor and the promotion loop

The craft floor is a growing, platform-level list of machine-checked rules,
not designed upfront, built one promoted correction at a time: no text under
14px, sentence case, scrims over imagery, no orphaned words in headlines,
one type scale, consistent motion across sibling surfaces, and whatever
comes next.

The promotion rule: when a human repeats a correction, it becomes a
machine-checked rule immediately. A third occurrence of the same correction
is a system failure, not a reminder. This matters more inside a factory than
in a solo practice, client feedback is a high-volume correction stream, and
without the promotion loop, project forty inherits project one's mistakes.

---

## 13. How we collaborate

These rituals apply most directly to client-in-the-loop mode and to the
human-adjacent parts of lights-out mode (escalations, contract governance).
In **backlog refinement** we pressure-test requirements against the intake
spec and record gaps as assumptions, not blockers. In **sprint planning** we
size design work realistically. We run regular **design critiques** with
fresh context, separating "does it meet the jobs to be done" from personal
preference. **Three amigos** (design + build-agent output + PM/QA) align on
the build brief's acceptance checks before a build agent starts. In **demos
and retros** we show outcomes against intake's success signal and feed
learnings back into the craft floor through the promotion loop.

---

## 14. The tooling: agent + skills

This practice is encoded in a Cowork toolkit the whole team can use:

- **Prisma (UX/UI Design Agent)**, applies everything in this playbook end
  to end, across both intake paths and both operating modes.
- **design-dor-dod**, runs the intake spec and produces the Ready / Done
  verdicts.
- **frontend-stack-advisor**, recommends the front-end framework/library,
  mainly on Path B.
- **ia-user-flows**, defines information architecture and user flows
  covering every state; its state inventory feeds the prototype and design
  QA.
- **design-system**, produces and audits the design contract.
- **figma-intake**, Path A: extracts tokens, styles, and components from an
  existing Figma file or live product into the design contract, reconciled
  against the live product, no longer produces production code.
- **frontend-prototype**, generates the coded prototype and its companion
  build brief.
- **design-qa**, runs the layered, advisory QA pass with a severity-ranked
  log and the visual diff.
- **heuristic-evaluation**, audits usability against Nielsen's heuristics
  with severity ratings; used before designing (Path A / existing
  competitors) and as expert review.
- **accessibility-audit**, runs a WCAG 2.2 AA audit with prioritized fixes,
  early where possible.
- **feedback-triage**, routes lights-out mode's end-of-run feedback to a
  contract change, a prototype change, a build defect, or a new
  requirement.
- **animation-vocabulary, apple-design, emil-design-eng,
  find-animation-opportunities, improve-animations, review-animations**,
  vendored from `emilkowalski/skills` (MIT license) for the motion mechanics
  a deterministic script can't check. Each carries a house rule: the design
  contract's stated motion personality wins on any aesthetic call.

See `docs/tools.md` for the recommended external tools (design contract
generation, the deterministic hook, the visual-diff loop, motion) and the
house-rule adoption pattern for each. Prisma is the judgment for design work
end to end; each skill is the repeatable procedure for a specific task.

---

## 15. Quick reference

**Starting a task?** Run intake against the spec. Complete or Complete with
assumptions, go. Blocked only for missing data, users, or jobs to be done.

**Finishing a task?** Run the DoD, the layered QA pass, and the feel
verdict before handoff.

**Adding a UI pattern?** Check the design contract first. Reuse, then
extend, then (only if necessary) propose a new component through
governance.

**Handing off?** Deliver the design contract, the prototype, and the build
brief, then prove a build matches with a visual diff, not a description.

**Which mode?** Confirm lights out or client in the loop at intake, as a
commercial decision, never a silent default.

**Unsure about accessibility?** Run the accessibility audit early, AA is the
floor, and regulated work may need more.
