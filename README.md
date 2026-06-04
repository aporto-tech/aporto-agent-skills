# Aporto Agent Skills

Thousands of agent skills, one Aporto entrypoint, zero catalog bloat in context.

AI agents should not carry a giant prompt library around. A useful agent needs a
small way to discover the right expert instruction at the moment it needs it,
load only that instruction, and run real capabilities through Aporto when the
task leaves the chat window.

Aporto Agent Skills is the open-source skill registry for that workflow.

## Why This Exists

Most agent skill libraries make one of two tradeoffs:

- Load many prompts/tools into context and pay for noise on every request.
- Keep everything local and force every user to manage search, embeddings, and
  updates themselves.

Aporto keeps the catalog outside the model context. This repository is the
public source of truth for MD skills. Aporto indexes it server-side, stores
embeddings, and exposes a tiny discover/load/run API.

## Quick Start

Use the Aporto MCP/client package or call the API directly.

```txt
discover_agent_skills("review this PR before merge")
load_agent_skill("gstack-pr-review")
run_capability("run code review", params)
```

The agent sees a few Aporto tools, not thousands of skills.

## How It Works

1. Skills live in this repository as `SKILL.md` files.
2. Aporto syncs the repository on a monthly cadence and on manual release.
3. Aporto computes embeddings from `name`, `description`, `tags`,
   `when_to_use`, and examples.
4. Agents call Aporto `discover`, not the raw catalog.
5. Aporto returns a short ranked list.
6. The agent loads one selected MD skill.
7. If the skill needs real execution, the agent runs an Aporto capability.

## Embeddings

The default production embedding model should be `text-embedding-3-large`.

Discovery quality matters more than saving a small amount per index build. Most
users will discover occasionally, then reuse saved skill IDs or direct capability
IDs in repeated workflows.

Recommended retrieval pipeline:

```txt
query -> text-embedding-3-large -> vector search -> metadata filters -> rerank -> top-N summaries
```

## API Surface

Keep discovery separate from execution:

```txt
POST /api/agent-skills/discover
GET  /api/agent-skills/:id

POST /api/routing/run
GET  /api/skill-runs/:id
```

`agent-skills` is the instruction layer. `routing/run` is the execution layer.

## Repository Shape

```txt
skills/
  engineering/
  product/
  design/
  security/
  research/
schema/
  skill.schema.json
registry/
  skills.generated.json
docs/
  update-policy.md
scripts/
  validate-skills.ts
  build-registry.ts
```

## Skill Contract

Every skill is a markdown file with frontmatter metadata used for indexing:

```md
---
id: gstack-pr-review
name: PR Review
description: Review a code diff for bugs, regressions, trust boundary issues, and missing tests.
tags: [engineering, review, code-quality]
when_to_use:
  - Review a branch before merge
  - Check a pull request for production risks
required_capabilities:
  - repository_read
  - diff_analysis
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# PR Review

Use this skill when...
```

## Who This Is For

- Agent builders who want expert workflows without loading a huge catalog.
- Open-source maintainers who want reusable skill instructions.
- Aporto users who want MD skills plus real execution through the same gateway.
- Teams that want skill discovery, versioning, and updates handled centrally.

## Updating Skills

This repository stores our canonical snapshot. Upstream projects may change;
Aporto should not blindly hot-load upstream content into production.

Monthly update flow:

1. Fetch configured upstream sources.
2. Compare upstream skill metadata and body against our snapshot.
3. Generate a PR with added/changed/removed skills.
4. Run validation, safety checks, and retrieval evals.
5. Merge accepted updates.
6. Aporto backend syncs the merged repo and rebuilds embeddings.

See [docs/update-policy.md](docs/update-policy.md).

## License

This repository is intended to be open source. Each imported skill should include
source attribution when it is adapted from another project.

