---
id: gstack-debug-root-cause
name: Root Cause Debugging
description: Investigate an error systematically before implementing a fix.
tags: [debugging, root-cause, errors, investigation]
when_to_use:
  - Debug an error or broken behavior
  - Investigate why something stopped working
  - Avoid applying fixes before understanding the cause
required_capabilities:
  - repository_read
  - log_analysis
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Root Cause Debugging

Use this skill when an agent needs to debug a reported failure.

## Process

1. Reproduce or observe the failure.
2. Gather facts from logs, code, requests, config, and recent changes.
3. Form hypotheses only after evidence is collected.
4. Implement the smallest fix that addresses the root cause.
5. Verify the fix and explain why it works.

## Rule

Do not patch symptoms before identifying the root cause.

