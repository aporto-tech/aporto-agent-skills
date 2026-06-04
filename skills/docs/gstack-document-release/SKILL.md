---
id: gstack-document-release
name: Document Release
description: Update project documentation after a shipped change so docs match the actual implementation.
tags: [documentation, release, changelog, readme]
when_to_use:
  - Sync docs after code changes
  - Update README, changelog, or architecture docs
  - Prepare release notes
required_capabilities:
  - repository_read
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Document Release

Use this skill when documentation should be updated after implementation.

## Process

1. Read the diff and relevant docs.
2. Update docs to match shipped behavior.
3. Remove stale TODOs or claims.
4. Keep release notes specific and useful.
5. Avoid documenting unrelated future plans as shipped facts.

