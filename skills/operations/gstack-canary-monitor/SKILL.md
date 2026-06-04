---
id: gstack-canary-monitor
name: Canary Monitor
description: Monitor a live deployment for page failures, console errors, and visible regressions.
tags: [operations, deploy, monitoring, canary]
when_to_use:
  - Verify a deployment after release
  - Watch production for immediate regressions
  - Check console errors and page health
required_capabilities:
  - browser_automation
  - screenshot_capture
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Canary Monitor

Use this skill after a deployment needs live verification.

## Process

1. Load production routes that matter.
2. Check HTTP status, visible content, and console errors.
3. Compare against expected screenshots or behavior.
4. Watch for a defined period when needed.
5. Report anomalies and rollback risk.

