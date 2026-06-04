---
id: gstack-ship-pr
name: Ship PR
description: Prepare a code change for shipping by checking diff, tests, docs, versioning, and PR readiness.
tags: [shipping, release, pull-request, changelog]
when_to_use:
  - Prepare a branch for PR
  - Run final checks before shipping
  - Create a release-ready summary
required_capabilities:
  - repository_read
  - git_operations
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Ship PR

Use this skill when a code change is ready to be packaged for review or release.

## Process

1. Inspect the diff and base branch.
2. Run relevant tests or checks.
3. Update docs, changelog, or version files when needed.
4. Prepare a clear PR summary and test evidence.
5. Avoid mixing unrelated changes.

