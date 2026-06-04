---
id: gstack-devex-review
name: Developer Experience Review
description: Test onboarding, docs, CLI help, error states, and time-to-hello-world for developer-facing products.
tags: [devex, documentation, onboarding, cli]
when_to_use:
  - Audit developer onboarding
  - Test docs and getting started flow
  - Measure time to first successful result
required_capabilities:
  - browser_automation
  - documentation_read
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Developer Experience Review

Use this skill when an agent needs to test a developer-facing flow.

## Process

1. Start from the public docs or install instructions.
2. Try to reach a first successful result.
3. Measure friction, missing steps, confusing errors, and unclear copy.
4. Score the experience with evidence.
5. Recommend fixes that reduce time-to-success.

