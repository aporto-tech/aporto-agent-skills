---
id: gstack-security-audit
name: Security Audit
description: Audit infrastructure, dependencies, secrets, AI trust boundaries, and application security risks.
tags: [security, audit, owasp, threat-model, secrets]
when_to_use:
  - Run a security review
  - Check for exposed secrets or unsafe integrations
  - Threat model an app or AI workflow
required_capabilities:
  - repository_read
  - dependency_analysis
context_cost: high
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# Security Audit

Use this skill when an agent needs a security-focused review.

## Process

1. Check secrets, credentials, and client-side exposure.
2. Review dependency and supply-chain risks.
3. Inspect trust boundaries, especially around AI/tool execution.
4. Apply OWASP-style web app checks where relevant.
5. Report only defensible findings with impact and likely fix.

