---
name: heuristic-evaluation
description: >
  Evaluate a design or product against established usability heuristics
  (Nielsen's 10) and produce a severity-rated findings report. Use to audit an
  existing product or a competitor in research, or as an expert review of a new
  design alongside QA, triggers like "heuristic evaluation", "usability audit",
  "expert review", "assess this against Nielsen's heuristics", "what usability
  problems does this have?", or "review the current app before redesign". Sibling
  to accessibility-audit: this covers usability, that covers WCAG.
---

# Heuristic Evaluation

Assess an interface against recognized usability principles and return a
prioritized, severity-rated issue list. It's a fast, expert "discount usability"
method, not a substitute for testing with real users, but a strong complement.

## When to use
- **In research:** audit the current product (redesigns) or a competitor to
  surface usability problems and opportunities before designing.
- **As expert review:** critique a new design/build against principles, alongside
  `design-qa`, before or after usability testing.

## The heuristics (Nielsen's 10)
1. Visibility of system status.
2. Match between the system and the real world.
3. User control and freedom (undo/redo, exits).
4. Consistency and standards.
5. Error prevention.
6. Recognition rather than recall.
7. Flexibility and efficiency of use.
8. Aesthetic and minimalist design.
9. Help users recognize, diagnose, and recover from errors.
10. Help and documentation.

Extend with context-specific checks where relevant: mobile/touch ergonomics,
form design, data-table/dashboard density, and onboarding, but map each finding
back to a heuristic.

## How to run it
1. **Scope & context.** Define what you're evaluating (flows/screens), the target
   users, and the device/context. Ideally 2-3 evaluators review independently,
   then merge, it catches far more than one pass.
2. **Walk the key flows** as a user would, screen by screen, checking each against
   the heuristics.
3. **Log each issue** with: location, the heuristic(s) it violates, a description
   of the problem and its user impact, and a recommended fix.
4. **Rate severity** (Nielsen 0-4): 0 not a problem · 1 cosmetic · 2 minor ·
   3 major · 4 catastrophe. Factor frequency, impact, and persistence.
5. **Prioritize** the fixes: high-severity and high-frequency first.

## Output
A findings report as a table: `# | Location | Heuristic (SC) | Severity (0-4) |
Problem & user impact | Recommended fix`. Group by severity, lead with the worst,
and end with a short summary of themes and the top fixes. Note where a real
usability test is still needed to confirm.

## Template
Use the bundled `templates/heuristic-findings-log.csv` to record each finding
with its heuristic, Nielsen severity (0-4), user impact, and recommended fix.

## How it connects
- **Research:** findings feed problem framing, opportunities, and the redesign's
  old→new decisions (`ia-user-flows`).
- **design-qa:** use this as the expert-review lens; QA verifies states, system
  fidelity, and build parity, while this judges usability against principles.
- **accessibility-audit:** run alongside it, usability and accessibility overlap
  but are distinct; together they cover "usable" and "accessible."
