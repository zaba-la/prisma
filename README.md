# Prisma — Agente de Diseño UX/UI (Ballast Lane)

Prisma es el agente de diseño UX/UI de Ballast Lane: un partner de diseño senior
que cubre todo el ciclo de vida del producto (descubrimiento, arquitectura de
información, flujos, wireframes, UI de alta fidelidad, motion, sistema de
diseño, documentación, QA y handoff a desarrollo). Este repositorio es el
toolkit que el equipo de diseño usa dentro de Claude Code / Cowork: el agente,
sus skills y el playbook humano que documenta los mismos estándares.

## Estructura del repositorio

```
.
├── agents/
│   └── prisma.md                # Definición del agente Prisma
├── skills/                      # 9 skills invocables, una carpeta por skill
│   ├── accessibility-audit/
│   ├── design-dor-dod/
│   ├── design-qa/
│   ├── design-system/
│   ├── figma-to-frontend/
│   ├── frontend-prototype/
│   ├── frontend-stack-advisor/
│   ├── heuristic-evaluation/
│   └── ia-user-flows/
└── docs/
    ├── uxui-design-playbook.md  # Playbook legible para el equipo (humano)
    └── assets/
        ├── prisma-process.png
        └── prisma-process.svg
```

Cada skill vive en su propia carpeta con un `SKILL.md` (instrucciones que sigue
el agente) y, cuando aplica, una carpeta `templates/` con checklists o logs en
formato `.md`/`.csv` listos para usar.

## Cómo instalarlo

Prisma está pensado para Claude Code / Cowork. Copia el agente y los skills a
tu configuración de Claude:

**Para uso personal (disponible en todos tus proyectos):**

```bash
mkdir -p ~/.claude/agents ~/.claude/skills
cp agents/prisma.md ~/.claude/agents/
cp -R skills/* ~/.claude/skills/
```

**Para un proyecto específico (solo disponible en ese repo):**

```bash
mkdir -p .claude/agents .claude/skills
cp /ruta/a/este/repo/agents/prisma.md .claude/agents/
cp -R /ruta/a/este/repo/skills/* .claude/skills/
```

Después de copiar, reinicia Claude Code (o abre una nueva sesión) para que
detecte el agente y los skills nuevos.

## Catálogo de skills

| Skill | Úsalo para... |
|---|---|
| [`frontend-stack-advisor`](skills/frontend-stack-advisor/SKILL.md) | Elegir el framework/librería de front-end en discovery, antes de fijar tokens o UI de alta fidelidad. |
| [`ia-user-flows`](skills/ia-user-flows/SKILL.md) | Definir arquitectura de información y flujos de usuario cubriendo todos los estados. |
| [`design-system`](skills/design-system/SKILL.md) | Crear, auditar, extender o consumir un sistema de diseño (tokens, componentes, gobernanza). |
| [`frontend-prototype`](skills/frontend-prototype/SKILL.md) | Generar un prototipo de front-end funcional como base lista para desarrollo. |
| [`figma-to-frontend`](skills/figma-to-frontend/SKILL.md) | Convertir un diseño de Figma finalizado en código de producción. |
| [`design-qa`](skills/design-qa/SKILL.md) | Revisión de calidad en dos pasadas: pre-handoff y post-implementación. |
| [`heuristic-evaluation`](skills/heuristic-evaluation/SKILL.md) | Evaluar un producto contra las 10 heurísticas de Nielsen, con hallazgos por severidad. |
| [`accessibility-audit`](skills/accessibility-audit/SKILL.md) | Auditar accesibilidad contra WCAG 2.2 AA con remediación priorizada. |
| [`design-dor-dod`](skills/design-dor-dod/SKILL.md) | Generar o validar el Definition of Ready / Definition of Done de una tarea de diseño. |

Prisma es el criterio para el trabajo de diseño de punta a punta; cada skill es
el procedimiento repetible para una tarea puntual. Usa a Prisma cuando
necesites pensamiento de diseño; usa un skill cuando necesites un checkpoint,
auditoría o conversión específica de forma consistente.

## Playbook

[`docs/uxui-design-playbook.md`](docs/uxui-design-playbook.md) es la versión
legible para humanos de los mismos estándares que sigue Prisma: en qué
creemos, los tres modos de proyecto, el ciclo de vida de diseño, DoR/DoD,
sistema de diseño, motion, documentación, QA, accesibilidad y handoff. Úsalo
para onboarding de nuevos miembros del equipo y como referencia en tickets.

## Diagrama del proceso

![Proceso de diseño Prisma](docs/assets/prisma-process.svg)

## Contribuir

- El agente (`agents/prisma.md`) y el playbook (`docs/uxui-design-playbook.md`)
  deben mantenerse alineados: si cambias un estándar en uno, actualízalo en el
  otro.
- Los skills nuevos van en `skills/<nombre>/SKILL.md`, siguiendo el mismo
  formato de frontmatter (`name`, `description` con triggers claros) que los
  existentes.
- Prisma nunca usa rayas (— ni –) en su output; si editás el agente o el
  playbook, mantené ese estilo de puntuación.
