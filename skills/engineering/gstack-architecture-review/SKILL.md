---
id: gstack-architecture-review
name: Architecture Review
description: Review a technical plan for architecture, data flow, edge cases, testing, and implementation risk.
tags: [engineering, architecture, planning, technical-review]
when_to_use:
  - Review architecture before implementation
  - Lock an execution plan
  - Catch data flow, edge case, and test coverage gaps
required_capabilities:
  - repository_read
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Architecture Review

Use this skill when an agent needs to review a technical plan before coding.

## Process

1. Map the data flow and ownership boundaries.
2. Identify edge cases, failure modes, and rollback needs.
3. Check whether the plan fits the existing system.
4. Specify test coverage proportional to risk.
5. Produce an implementation-ready plan.

