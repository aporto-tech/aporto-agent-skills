# Update Policy

Aporto Agent Skills uses repository snapshots, not live upstream loading.

## Why

Agent skills are instructions. Updating them can change behavior, safety, cost,
and quality. We should not let an upstream repository change production behavior
without review.

## Cadence

Default cadence: monthly.

Emergency updates may be merged sooner for security, broken instructions, or
high-value new skills.

## Monthly Sync

1. Fetch configured upstream repositories.
2. Parse `SKILL.md` files and metadata.
3. Normalize into Aporto skill schema.
4. Compare against the current repository snapshot.
5. Open a PR with:
   - added skills;
   - changed skills;
   - removed or renamed upstream skills;
   - metadata changes;
   - source attribution.
6. Run validation.
7. Run retrieval evals against known intents.
8. Merge reviewed changes.
9. Rebuild Aporto server-side embeddings.

## Production Indexing

The Aporto backend indexes only merged repository state.

Recommended index fields:

- `name`
- `description`
- `tags`
- `when_to_use`
- `required_capabilities`
- short examples

Recommended model: `text-embedding-3-large`.

## Deletions

Do not immediately delete skills from production when upstream removes them.
Mark them as deprecated first unless the removal is security-related.

## Source Attribution

Imported skills must include a `source` field in frontmatter.

