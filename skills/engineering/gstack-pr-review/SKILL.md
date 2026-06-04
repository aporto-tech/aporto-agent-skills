---
id: gstack-pr-review
name: PR Review
description: Review a code diff before merge for bugs, regressions, trust boundary issues, and missing tests.
tags: [engineering, review, code-quality, pull-request]
when_to_use:
  - Review a branch before merging
  - Check a pull request for production risks
  - Find missing tests or behavioral regressions
required_capabilities:
  - repository_read
  - diff_analysis
context_cost: medium
source:
  name: gstack
  url: https://github.com/garrytan/gstack
---

# PR Review

Use this skill when an agent needs to review code before it lands.

## Process

1. Read the diff against the base branch.
2. Prioritize concrete bugs, regressions, trust boundary issues, data safety, and missing tests.
3. Report findings first, ordered by severity.
4. Include file and line references when available.
5. Keep summaries secondary to findings.

## Output

Return a concise review with findings, open questions, and residual risk.

