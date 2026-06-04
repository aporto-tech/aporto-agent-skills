---
id: linkedin-identity-research
name: LinkedIn Identity Research
description: Find or verify professional identity from email, name, company, role, or public web signals.
tags: [linkedin, research, identity, enrichment, sourcing]
when_to_use:
  - Find a likely LinkedIn profile from an email address
  - Verify that a person, company, and role belong together
  - Prepare structured professional identity context for outreach
required_capabilities:
  - web_search
  - linkedin_lookup
context_cost: medium
---

# LinkedIn Identity Research

Use this skill when an agent needs to find or verify a professional profile
without loading a large sourcing playbook into context.

## Process

1. Extract known signals: email, name, company, domain, role, location, and any
   public profile hints.
2. Search for the strongest identity match using the smallest useful query.
3. Compare profile, company, role, and domain evidence before returning a match.
4. Return uncertainty explicitly when signals conflict.

## Output

Return a compact JSON object with likely profile URL, confidence, evidence, and
open questions.

