# API Client Generation Skill

Workshop repository for **Stop Re-Prompting: How Reusable AI Skills Make Vibe Coding Actually Work**.

The installable Skill starts with retry conventions completed. During the workshop, attendees complete authentication, error-handling, and pagination rules, then compare the generated clients.

## Install the Skill

From the project where you want to use it:

```bash
npx skills add ThatCoolGuyyy/api-client-generation-skill --skill api-client-generation
```

The CLI detects supported coding agents and asks where to install the Skill. The default installation is project-scoped; add `--global` to use it across projects.

## Workshop files

- `skills/api-client-generation/SKILL.md` — installable starter
- `demo/openapi.yaml` — shared Notes API contract
- `demo/PROMPT.txt` — shared generation prompt
- `demo/COMPARISON_CHECKLIST.md` — observable comparison criteria
- `workshop/REFERENCE_SKILL.md` — completed instructor reference, revealed after the exercise

