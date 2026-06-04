---
id: gstack-unfreeze
name: Unfreeze
description: Clear the freeze boundary set by /freeze, allowing edits to all directories again. Use when you want to widen edit scope without ending the session. Use when asked to \"unfreeze\", \"unlock edits\", \"remove freeze\", or \"allow all edits\". (gstack)
tags: [gstack]
when_to_use:
  - unfreeze
  - unlock edits
  - remove freeze
  - allow all edits
required_capabilities:
  []
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
  path: unfreeze/SKILL.md
---

# Unfreeze

Clear the freeze boundary set by /freeze, allowing edits to all directories again. Use when you want to widen edit scope without ending the session. Use when asked to "unfreeze", "unlock edits", "remove freeze", or "allow all edits". (gstack)

## Source Snapshot

This Aporto skill is adapted from the gstack open-source skill at `unfreeze/SKILL.md`. Use it as an instruction layer. If real execution is needed, call an Aporto capability through the routing API.

## Original Skill Body

```md
---
name: unfreeze
version: 0.1.0
description: |
  Clear the freeze boundary set by /freeze, allowing edits to all directories
  again. Use when you want to widen edit scope without ending the session.
  Use when asked to "unfreeze", "unlock edits", "remove freeze", or
  "allow all edits". (gstack)
triggers:
  - unfreeze edits
  - unlock all directories
  - remove edit restrictions
allowed-tools:
  - Bash
  - Read
---
<!-- AUTO-GENERATED from SKILL.md.tmpl — do not edit directly -->
<!-- Regenerate: bun run gen:skill-docs -->

# /unfreeze — Clear Freeze Boundary

Remove the edit restriction set by `/freeze`, allowing edits to all directories.

```​bash
mkdir -p ~/.gstack/analytics
echo '{"skill":"unfreeze","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'","repo":"'$(basename "$(git rev-parse --show-toplevel 2>/dev/null)" 2>/dev/null || echo "unknown")'"}'  >> ~/.gstack/analytics/skill-usage.jsonl 2>/dev/null || true
```​

## Clear the boundary

```​bash
eval "$(~/.claude/skills/gstack/bin/gstack-paths)"
STATE_DIR="$GSTACK_STATE_ROOT"
if [ -f "$STATE_DIR/freeze-dir.txt" ]; then
  PREV=$(cat "$STATE_DIR/freeze-dir.txt")
  rm -f "$STATE_DIR/freeze-dir.txt"
  echo "Freeze boundary cleared (was: $PREV). Edits are now allowed everywhere."
else
  echo "No freeze boundary was set."
fi
```​

Tell the user the result. Note that `/freeze` hooks are still registered for the
session — they will just allow everything since no state file exists. To re-freeze,
run `/freeze` again.

```
