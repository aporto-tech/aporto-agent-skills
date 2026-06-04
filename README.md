# Aporto Agent Skills

Open-source MD skill registry for AI agents.

Agents should not load the full catalog into context. They connect one Aporto
entrypoint, discover relevant skills at runtime, load only the selected
`SKILL.md`, and execute real capabilities through Aporto when needed.

## MVP Flow

1. Agent calls `discover_agent_skills` with an intent.
2. Aporto searches server-side embeddings built from this repository.
3. Agent receives a small ranked list of matching skills.
4. Agent calls `load_agent_skill` for one selected skill.
5. If action is required, agent calls an Aporto capability through `run`.

## Repository Shape

```txt
skills/
  research/
    linkedin-identity-research/SKILL.md
schema/
  skill.schema.json
registry/
  skills.generated.json
scripts/
  validate-skills.ts
  build-registry.ts
```

## Skill Contract

Every skill is a markdown file with frontmatter metadata used for indexing:

```md
---
id: linkedin-identity-research
name: LinkedIn Identity Research
description: Find or verify professional identity from email, name, company, or role.
tags: [linkedin, research, identity, enrichment]
when_to_use:
  - Find a likely LinkedIn profile from an email address
  - Verify professional identity before outreach
required_capabilities:
  - web_search
  - linkedin_lookup
context_cost: medium
---

# LinkedIn Identity Research

Use this skill when...
```

