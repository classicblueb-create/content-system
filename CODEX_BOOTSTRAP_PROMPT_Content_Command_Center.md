# Codex Bootstrap Prompt — Content Command Center

You are building **Content Command Center**, an AI Content Production OS.

Read `Content_Command_Center_PRD_Codex.md` as the product source of truth.

## Build principles

1. Build vertical slices.
2. Keep AI providers behind interfaces.
3. Project context is mandatory for generation.
4. Design instructions are stored separately from prompts.
5. Every AI call creates an AgentRun record.
6. Every output stores lineage metadata.
7. Use typed schemas and validate AI outputs.
8. Human approval must exist before publish automation.
9. Reuse existing work before generating new work.
10. Avoid autonomous agent chat loops. Prefer deterministic workflows.

## First implementation milestone

Create:

- Next.js
- TypeScript
- Tailwind
- PostgreSQL
- Auth
- Project switcher
- Navigation
- Dashboard shell
- Placeholder routes

Routes:

```text
/
projects
design
research
ideas
content
visual
calendar
library
system/runs
```

UI direction:

- light
- cream / warm white
- black text
- orange accent
- rounded cards
- clean SaaS UI
- Kanit for Thai headings when available in the app
- no handwriting fonts

## Do not implement AI yet.

First deliver:
1. proposed folder structure
2. database setup
3. base layout
4. navigation
5. empty route pages
6. reusable Card / Section / StatusBadge / ProjectSwitcher components

After completing the milestone:
- show changed files
- explain architecture
- list next 5 tasks
- do not silently add unrelated features
