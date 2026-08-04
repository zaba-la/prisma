# Prisma: UX/UI Design Agent

Prisma is a UX/UI design agent: one stage in a multi-agent build pipeline,
not a solitary designer who owns a project end to end. It takes
requirements in (no primary discovery, that happens upstream) and produces
three artifacts, a **design contract**, a coded **prototype**, and a **build
brief**, then proves whether a build matches them with a visual diff.
Prisma never writes production code and never blocks a build agent,
findings travel as severity-tagged recommendations. This repository is the
toolkit the design team uses inside Claude Code / Cowork: the agent, its
skills, and the human-readable playbook that documents the same standards.

## Repository structure

```
.
├── agents/
│   └── prisma.md                # Prisma agent definition
├── skills/                      # 16 invocable skills, one folder per skill
│   ├── accessibility-audit/
│   ├── design-dor-dod/
│   ├── design-qa/
│   ├── design-system/
│   ├── feedback-triage/
│   ├── figma-intake/
│   ├── frontend-prototype/
│   ├── frontend-stack-advisor/
│   ├── heuristic-evaluation/
│   ├── ia-user-flows/
│   ├── animation-vocabulary/     # vendored, see "Vendored skills" below
│   ├── apple-design/             # vendored
│   ├── emil-design-eng/          # vendored
│   ├── find-animation-opportunities/  # vendored
│   ├── improve-animations/       # vendored
│   └── review-animations/        # vendored
├── LICENSES/                    # Licenses for vendored third-party skills
│   └── emilkowalski-skills-LICENSE.txt
└── docs/
    ├── uxui-design-playbook.md  # Human-readable team playbook
    ├── intake-spec.md           # What a requirements handoff must contain
    ├── craft-floor.md           # The platform-level, machine-checked rule list
    ├── design-fidelity-bar.md   # Provisional definition of "faithful to the design"
    ├── tools.md                 # Recommended external tools and the adoption rule
    └── assets/
        ├── prisma-process.png
        └── prisma-process.svg
```

Each skill lives in its own folder with a `SKILL.md` (the instructions the
agent follows) and, where relevant, a `templates/` folder with ready-to-use
checklists or logs in `.md`/`.csv` format.

## How to install it

Prisma is built for Claude Code / Cowork. Copy the agent and skills into
your Claude configuration:

**For personal use (available across all your projects):**

```bash
mkdir -p ~/.claude/agents ~/.claude/skills
cp agents/prisma.md ~/.claude/agents/
cp -R skills/* ~/.claude/skills/
```

**For a specific project (available only in that repo):**

```bash
mkdir -p .claude/agents .claude/skills
cp /path/to/this/repo/agents/prisma.md .claude/agents/
cp -R /path/to/this/repo/skills/* .claude/skills/
```

After copying, restart Claude Code (or start a new session) so it picks up
the new agent and skills.

## Skills catalog

| Skill | Use it to... |
|---|---|
| [`design-dor-dod`](skills/design-dor-dod/SKILL.md) | Run intake against the intake spec and return Ready / Not Ready, then validate the Definition of Done. |
| [`figma-intake`](skills/figma-intake/SKILL.md) | Intake path A: extract the design contract from an existing Figma file or live product, no production code. |
| [`frontend-stack-advisor`](skills/frontend-stack-advisor/SKILL.md) | Choose the front-end framework/library, mainly on intake path B, before locking tokens or high-fidelity UI. |
| [`ia-user-flows`](skills/ia-user-flows/SKILL.md) | Define information architecture and user flows covering every state. |
| [`design-system`](skills/design-system/SKILL.md) | Produce or audit the design contract (tokens, components, governance). |
| [`frontend-prototype`](skills/frontend-prototype/SKILL.md) | Build the coded prototype (the contract a build is judged against) and its companion build brief. |
| [`design-qa`](skills/design-qa/SKILL.md) | Run the advisory, layered QA pass: pre-handoff and a build-vs-prototype visual diff. |
| [`heuristic-evaluation`](skills/heuristic-evaluation/SKILL.md) | Evaluate a product against Nielsen's 10 heuristics, with severity-rated findings. |
| [`accessibility-audit`](skills/accessibility-audit/SKILL.md) | Audit accessibility against WCAG 2.2 AA, run early wherever possible. |
| [`feedback-triage`](skills/feedback-triage/SKILL.md) | In lights-out mode, route mixed end-of-run feedback to a contract change, prototype change, build defect, or new requirement. |

Prisma is the judgment for design work end to end; each skill is the
repeatable procedure for a specific task. Use Prisma when you need design
thinking; reach for a skill when you need a specific checkpoint, audit, or
conversion done consistently.

### Vendored skills (motion)

These six come from [emilkowalski/skills](https://github.com/emilkowalski/skills)
(MIT license, see `LICENSES/emilkowalski-skills-LICENSE.txt`), for the one
dimension a deterministic check can't cover. Each carries a "Prisma house
rule" appended at the end of its `SKILL.md`: it owns the mechanics, the
design contract's stated motion personality wins on any aesthetic call. Two
of the source repo's skills (`pick-ui-library`, `prototype`) were left out on
purpose, they duplicate `frontend-stack-advisor` and the multi-concept flow
already in this toolkit.

| Skill | Use it to... |
|---|---|
| [`find-animation-opportunities`](skills/find-animation-opportunities/SKILL.md) | Sweep an interface for moments that would genuinely benefit from motion, and propose exact values. Read-only. |
| [`improve-animations`](skills/improve-animations/SKILL.md) | Audit a codebase's motion and produce prioritized, self-contained fix plans. Read-only. |
| [`review-animations`](skills/review-animations/SKILL.md) | Review animation code in a diff against a ten-point craft bar. Default to flagging. |
| [`animation-vocabulary`](skills/animation-vocabulary/SKILL.md) | Turn a vague description of a motion effect ("the bouncy thing") into its exact term. |
| [`apple-design`](skills/apple-design/SKILL.md) | Spring-based, interruptible motion physics: velocity, momentum, spatial continuity. |
| [`emil-design-eng`](skills/emil-design-eng/SKILL.md) | UI polish and component-craft judgment as a reference point, never a substitute for the design contract. |

## What Prisma produces

Every project converges on the same three artifacts, the only interface
between Prisma and the build agents downstream:

1. **Design contract**, tokens, type scale, spacing, color roles, motion
   rules, who it's for and how it should feel, plus the assumption register
   from intake. See `docs/intake-spec.md` and the `design-system` skill.
2. **Prototype**, the core experience built in the real system with
   realistic data. What a build is judged against.
3. **Build brief**, scope edges, acceptance checks a build agent can run on
   itself, and the edge states deliberately left open.

A build gets checked against these with a visual diff, scored against
[`docs/design-fidelity-bar.md`](docs/design-fidelity-bar.md), the
provisional definition of what "faithful to the design" means. It is marked
provisional on purpose: it is meant to be validated (and corrected) by
running it against a build with known, seeded deviations before it is
trusted, see the document itself for that test.

## Playbook

[`docs/uxui-design-playbook.md`](docs/uxui-design-playbook.md) is the
human-readable version of the same standards Prisma follows: what we
believe, the two intake paths, the two operating modes, the design
lifecycle, DoR/DoD, the design contract, motion, documentation, QA,
accessibility, and handoff. Use it for onboarding new team members and as a
reference in tickets.

## Recommended tools

[`docs/tools.md`](docs/tools.md) lists the external tools this toolkit
recommends adopting rather than rebuilding (design contract generation, a
deterministic edit-time check, the visual-diff loop, motion), and the house
rule for bounding any outside skill: it owns the mechanical part it was
built for, aesthetic decisions always come from the design contract.

## Process diagram

![Prisma design process](docs/assets/prisma-process.svg)

## Contributing

- The agent (`agents/prisma.md`) and the playbook
  (`docs/uxui-design-playbook.md`) must stay aligned: if you change a
  standard in one, update the other.
- New skills go in `skills/<name>/SKILL.md`, following the same frontmatter
  format (`name`, `description` with clear triggers) as the existing ones.
- Vendoring an outside skill: copy it unmodified, add an attribution comment
  after the frontmatter, append a "Prisma house rule" section at the end, and
  drop the source license in `LICENSES/`. See `docs/tools.md` for the full
  checklist and when to vendor vs. just link.
- Prisma never uses em dashes (—) or en dashes (–) in its output; keep that
  punctuation style when editing the agent, the playbook, or any skill.
