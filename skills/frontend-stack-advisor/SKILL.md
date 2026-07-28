---
name: frontend-stack-advisor
description: >
  Recommend or decide the front-end framework and UI library for a project based
  on platform, project type, and constraints. Use during project discovery /
  refinement, before locking design tokens or high-fidelity UI, triggers like
  "which framework should we use?", "recommend a UI library", "shadcn or MUI?",
  "what should we build this dashboard in?", "mobile app, Material or HIG?",
  or "pick the front-end stack". Produces a recommendation with rationale,
  alternatives, and trade-offs, decided with engineering; the outcome becomes a
  DoR constraint and the basis for the design system's token/component mapping.
---

# Front-end Stack Advisor

Decide the front-end framework/library early, in discovery or the first
refinement, because design tokens and components map to whatever is chosen, and
high-fidelity design shouldn't start before it's settled. The recommendation is
made **with engineering**, not imposed on them.

## Step 1: Gather the deciding inputs
- **Platform:** responsive web, native iOS, native Android, cross-platform
  mobile, desktop, embedded.
- **Project type:** admin/dashboard, data-dense enterprise app, consumer app,
  marketing/brand-forward site, internal tool, design-system/library itself.
- **Constraints:** existing codebase or design system, client/tech mandate, team
  skills and familiarity, timeline, licensing/budget, performance, accessibility
  target, theming needs (multi-brand / white-label / light-dark), SSR/SEO.

## Step 2: Map inputs to options (decision guide)
Treat these as strong defaults, not rules; the constraints above can override.

**React web app / dashboard / admin**
- **shadcn/ui + Tailwind + Radix**, you own the code, maximum brand
  flexibility, tokens map cleanly; great default when brand ≠ Material and the
  team wants control.
- **MUI (Material UI)**, batteries-included, fast, enterprise-friendly; best
  when the brand is close to Material or speed/coverage matters most.
- **Ant Design**, dense enterprise dashboards with lots of built-in components.
- **Chakra UI**, accessible, quick to build, good DX; lighter branding control
  than shadcn.

**Marketing / brand-forward web**, Tailwind + custom, or headless (Radix /
Headless UI) for full brand control; consider SSR (Next.js) for SEO.

**Native mobile**, iOS: **SwiftUI following Apple HIG**; Android: **Jetpack
Compose + Material 3**. Don't fight the platform's conventions.

**Cross-platform mobile**, React Native (React Native Paper for Material,
Tamagui, or NativeBase) or Flutter (Material / Cupertino). Choose by team skills
and how native the UX must feel.

**Existing design system / client mandate**, consume it; the advisor's job is to
confirm fit, surface gaps, and note risks rather than reopen the choice.

**Token portability / multi-brand / white-label**, favor headless + tokens
(shadcn/Radix + Tailwind, or a Style Dictionary token pipeline) so brands swap at
the token layer.

## Step 3: Produce the recommendation
Output: the recommended framework/library, one or two viable alternatives, the
rationale tied to the inputs, trade-offs, and implications for tokens, component
mapping, theming, and accessibility. Flag risks (licensing, lock-in, team ramp,
brand fit). Align to the platform's design language (Material on Android, HIG on
iOS) unless there's a deliberate reason not to.

## Step 4: Record the decision
Capture the decision (with engineering sign-off) as a DoR constraint and the
basis for the design system: tokens will map to this framework's theme config,
and components will mirror its API. Note the date and who decided.

## Notes
- Team familiarity and existing code are legitimate, often decisive factors, the "best" library the team can't maintain is the wrong one.
- Pair with `design-system` (tokens/components map to the chosen stack) and
  `frontend-prototype` (validate the choice with a thin coded slice).
