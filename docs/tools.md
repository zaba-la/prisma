# Tool Ecosystem

Prisma's job is judgment: the design contract, the prototype, the build
brief, and proof that a build matches. Where a well-scoped external tool
already does part of the mechanical work, adopt it instead of building an
equivalent. This list is a starting point, not an endorsement to integrate
blindly, evaluate each one against the project's actual constraints before
relying on it.

| Tool | Use it for |
|---|---|
| [impeccable](https://impeccable.style) | Three pieces of this system off the shelf: `init`/`document` to generate and maintain the per-project design contract, a deterministic edit-time hook, and critique plus audit for heuristics, accessibility, performance, and responsive behavior. |
| [shadcn/ui](https://ui.shadcn.com) | The default component layer, especially on intake Path B (no existing Figma or product). Prototype and build sharing the same components is what makes the visual diff in `design-qa` meaningful instead of approximate. |
| [Figma community skills](https://figma.com/community/skills) | Intake Path A. Design context, variables, screenshots, Code Connect. Use these to pull the design contract out of an existing Figma file, never treat the Figma file itself as the prototype. |
| [Apple HIG](https://developer.apple.com/design/human-interface-guidelines) | Creation-time grounding and rubric depth for judgment critique, on top of whatever the design contract already specifies. |
| [emilkowalski/skills](https://github.com/emilkowalski/skills) | Motion, the one dimension that resists deterministic checks. Note the overlap: its `pick-ui-library` covers the same ground as `frontend-stack-advisor`, and its `prototype` flow covers the multi-concept request used in the client-in-the-loop mode, both already exist in this toolkit. |
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
