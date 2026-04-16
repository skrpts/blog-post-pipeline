---
type: skill
id: content-briefing
title: Content Briefing
description: "Creates structured briefs for writers and content producers"
tags: [Production, Content, Optimisation]
context_params:
  target_audience:
    label: "Target Audience"
    description: "Who this content is for"
    default: ""
    required: true
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Produces detailed content briefs covering angle, structure, key points, SEO targets, and reference material.

## When to Use

- Commissioning articles from freelance writers
- Briefing internal content team members
- Standardising content quality across contributors

## Inputs

Topic, target keyword(s), audience persona, desired length, reference URLs

## Outputs

Structured brief: working title, angle, outline with H2/H3 headings, key points to cover, target keyword placement, competitor references, tone guidance
