# Product Plan

## Decision Summary

- Use `text-embedding-3-large` for production discovery.
- Store embeddings on Aporto servers, not in the client.
- Keep MD skills in this repository as the canonical open-source snapshot.
- Keep backend endpoints inside `app.aporto` for MVP.
- Make MCP optional. API-first is the product; MCP is an adapter for agent hosts.
- Update upstream skill sources monthly through reviewed PRs.

## API Boundaries

Separate instruction discovery from execution.

### Agent Skills API

Instruction layer:

```txt
POST /api/agent-skills/discover
GET  /api/agent-skills/:id
GET  /api/agent-skills/:id/summary
```

Use this when the agent needs to find or load a markdown instruction.

### Capability Routing API

Execution layer:

```txt
POST /api/routing/run
GET  /api/skill-runs/:id
```

Use this when the agent needs real work: model calls, scraping, media generation,
browser automation, files, or other paid capabilities.

## Saved IDs

Discovery should not be required on every run.

Expected usage:

1. First task: agent calls `discover_agent_skills`.
2. Agent or application stores the chosen `skill_id`.
3. Repeated workflow calls `load_agent_skill(skill_id)` or jumps directly to
   `run_capability` with known capability IDs.

This makes `text-embedding-3-large` the right default: discovery quality matters
more than saving a small amount on infrequent searches.

## MVP

1. Add DB tables in `app.aporto`:
   - `agent_skills`
   - `agent_skill_versions`
   - `agent_skill_embeddings`
   - `agent_skill_sources`
2. Add repository sync job for `aporto-tech/aporto-agent-skills`.
3. Parse frontmatter and `SKILL.md` body.
4. Generate embeddings with `text-embedding-3-large`.
5. Add `POST /api/agent-skills/discover`.
6. Add `GET /api/agent-skills/:id`.
7. Add API docs and examples.
8. Add optional MCP package that wraps those endpoints.
9. Add 50 initial skills.
10. Add monthly upstream sync PR workflow.

## Full Product

- reranker after vector search;
- category and pack filters;
- private team skills;
- skill version pinning;
- skill deprecation flow;
- discovery analytics;
- eval set for search quality;
- GitHub import bot;
- contributor validation bot;
- safety review for imported instructions;
- UI in `app.aporto` for browsing skills;
- saved skill IDs per integration;
- skill-to-capability binding;
- monthly upstream release notes;
- optional local fallback search for offline development.

## Database

Use the existing `app.aporto` database for MVP.

Do not create a separate backend database until there is a real scaling reason.
The Aporto app already owns API keys, billing, routing, and execution logs.
Keeping agent skills in the same backend avoids split auth and split billing.

## MCP

MCP is useful but not mandatory.

Reasons to build it:

- many agent clients prefer tool calls over raw HTTP;
- it gives users one copy-paste config block;
- it keeps the visible tool surface tiny;
- it maps naturally to discover/load/run/get-result.

Reasons not to make it the core:

- MCP clients differ;
- API users should not need MCP;
- backend discovery and embeddings should remain server-side.

The product should be API-first and MCP-compatible.

