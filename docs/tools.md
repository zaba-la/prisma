# Tool Ecosystem

Prisma's job is judgment: the design contract, the prototype, the build
brief, and proof that a build matches. Where a well-scoped external tool
already does part of the mechanical work, adopt it instead of building an
equivalent. This list is a starting point, not an endorsement to integrate
blindly, evaluate each one against the project's actual constraints before
relying on it.

| Tool | Use it for |
|---|---|
| [impeccable](https://impeccable.style) | Three pieces of this system off the shelf: `init`/`document` to generate and maintain the per-project design contract, a deterministic edit-time hook, and critique plus audit for heuristics, accessibility, performance, and responsive behavior. Install as a Claude Code plugin: `/plugin marketplace add pbakaus/impeccable`, not vendored into this repo, it manages its own updates. |
| [shadcn/ui](https://ui.shadcn.com) | The default component layer, especially on intake Path B (no existing Figma or product). Prototype and build sharing the same components is what makes the visual diff in `design-qa` meaningful instead of approximate. |
| [Figma community skills](https://figma.com/community/skills) | Intake Path A. Design context, variables, screenshots, Code Connect. Use these to pull the design contract out of an existing Figma file, never treat the Figma file itself as the prototype. Loaded via Figma's own MCP/plugin, not vendored here. |
| [Apple HIG](https://developer.apple.com/design/human-interface-guidelines) | Creation-time grounding and rubric depth for judgment critique, on top of whatever the design contract already specifies. |
| [emilkowalski/skills](https://github.com/emilkowalski/skills) | Motion, the one dimension that resists deterministic checks. Vendored into `skills/` (MIT license, see `LICENSES/emilkowalski-skills-LICENSE.txt`): `animation-vocabulary`, `apple-design`, `emil-design-eng`, `find-animation-opportunities`, `improve-animations`, `review-animations`. Its `pick-ui-library` and `prototype` skills were left out, they cover the same ground as `frontend-stack-advisor` and the multi-concept flow already in this toolkit. |
| [agent-browser](https://github.com/vercel-labs/agent-browser) | The agent's own render, screenshot, fix, re-screenshot loop. A fast CLI over the DevTools Protocol with an accessibility-tree snapshot. |
| [Playwright](https://playwright.dev) | The acceptance checks written into the build brief, running repeatably in CI. |

## Making the visual diff real

`agent-browser` and Playwright together are what make `design-qa`'s
post-implementation pass real: screenshot the prototype and the build at the
same viewports, diff them, attach the comparison. A QA claim without a
comparison image is a sentence, not evidence.

## Adoption rule

Bound every outside skill with a house rule written inside the skill file
that adopts it: the outside skill owns the mechanical part it was built for
(a presentation skill owns the shell, viewport, navigation, transitions,
reduced-motion handling), and it is explicitly forbidden from making
aesthetic decisions, those always come from the project's design contract.
Adopt the machinery. Keep the taste in the contract.

## Vendoring a skill into this repo

When a skill is worth vendoring rather than just linking (as with
`emilkowalski/skills` above):

1. Copy the files unmodified into `skills/<name>/`.
2. Add an attribution comment (source repo, license, "unmodified except for
   the Prisma house rule section") right after the frontmatter.
3. Append a "Prisma house rule" section at the end of the file, stating what
   this skill owns and what always defers to the design contract instead.
4. Copy the source license into `LICENSES/<repo>-LICENSE.txt` and list the
   skill in the table above.

Skills that manage their own install/update mechanism (a Claude Code plugin
marketplace entry, a Figma-hosted MCP skill) are linked, not vendored, so
they keep getting updates from their source instead of going stale here.
