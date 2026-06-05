# Skill Authoring Rules

This repository stores Aporto's canonical markdown agent skills. The backend
indexes merged repository state and exposes discovery through Aporto, so every
skill must be clear, attributed, and safe to load as one focused instruction.

## Core Model

Aporto separates three things:

- **Concept**: the shared job-to-be-done, such as `design-review`,
  `marketing-plan`, or `seo-audit`.
- **Source**: the author or instruction library variant for that concept, such
  as `gstack / Garry Tan` or `marketingskills / Corey Haines`.
- **Capability**: executable work run through Aporto, such as web search,
  scraping, image generation, analytics lookup, or LLM routing.

Use `source` for markdown skills. Do not call a markdown skill source a
provider. `provider` is reserved for executable APIs, models, and capability
backends.

## Where To Add Skills

Use this structure:

```txt
skills/
  <source-slug>/
    <skill-slug>/
      SKILL.md
```

Examples:

```txt
skills/gstack/design-review/SKILL.md
skills/marketingskills/marketing-plan/SKILL.md
skills/aporto/linkedin-identity-research/SKILL.md
```

Add or update packs in:

```txt
registry/packs.json
```

Packs are many-to-many. A skill can appear in several packs without duplicating
the markdown file.

## Duplicate Concepts

If a new upstream repository contains a skill that does the same job as an
existing skill, do not create a new concept. Add it as a new source variant.

Good:

```yaml
id: marketingskills-design-review
concept:
  id: design-review
  name: Design Review
source:
  slug: marketingskills
  author: Corey Haines
```

Bad:

```yaml
id: marketingskills-design-review
concept:
  id: marketing-design-review
```

The concept should describe the user need, not the author, repo, or category.

## Required Frontmatter

Every `SKILL.md` must start with frontmatter:

```yaml
---
id: marketingskills-marketing-plan
name: Marketing Plan
description: Build a comprehensive growth and go-to-market plan for a product, client, or company.
concept:
  id: marketing-plan
  name: Marketing Plan
tags: [marketingskills, marketing, growth, strategy]
when_to_use:
  - Build a 90-day or 12-month marketing roadmap
  - Create a go-to-market plan
required_capabilities:
  - marketing_strategy
  - web_research
context_cost: medium
source:
  slug: marketingskills
  name: marketingskills
  display_name: Marketing Skills
  author: Corey Haines
  url: https://github.com/coreyhaines31/marketingskills
  path: skills/marketing-plan/SKILL.md
  priority: 100
---
```

Keep `description` on one line. The current Aporto parser intentionally supports
a simple frontmatter subset.

## IDs

Use lowercase kebab-case.

- `id`: `<source-slug>-<skill-slug>`
- `concept.id`: shared job-to-be-done, without source prefix when possible
- `source.slug`: source repository or maintainer slug

Examples:

```txt
id: gstack-design-review
concept.id: design-review
source.slug: gstack

id: marketingskills-seo-audit
concept.id: seo-audit
source.slug: marketingskills
```

## Body Format For Imported Skills

For imported upstream skills, use a snapshot format:

```md
# Skill Name

Use this Aporto agent skill when...

## Source Snapshot

This Aporto skill is adapted from <source> at `<path>`.

## Original Skill Body

```md
<original upstream SKILL.md>
```
```

Do not silently rewrite the upstream author's methodology. Normalize metadata
for discovery, but preserve the original instruction body with attribution.

## Capabilities

`required_capabilities` should describe capability needs, not exact vendors.

Good:

```yaml
required_capabilities:
  - web_research
  - analytics_review
  - content_generation
```

Bad:

```yaml
required_capabilities:
  - openrouter
  - fal
  - kie
```

Provider names belong in executable capability routing, not markdown skill
descriptions.

## Packs

After adding skills, update `registry/packs.json`.

Rules:

- Add specialty packs only when they help discovery.
- Keep packs broad enough to be useful: `marketing`, `engineering`, `security`.
- A skill may be in multiple packs.
- Do not duplicate a `SKILL.md` just to place it in another pack.

## Update Flow

1. Clone or fetch the upstream repository.
2. List upstream `SKILL.md` files.
3. Decide source slug and attribution.
4. Map duplicate jobs to existing `concept.id` values.
5. Add new source-variant files under `skills/<source-slug>/`.
6. Update `registry/packs.json`.
7. Validate parsing and discovery sync.
8. Commit and push.
9. Run Aporto backend sync to rebuild the indexed catalog.
