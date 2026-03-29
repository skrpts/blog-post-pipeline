---
type: prompt
id: generate-content-ideas
title: Generate Content Ideas
description: "Generates ranked content topic ideas for a given audience and niche"
tags: [Production, Audience, Content]
connections:
  - target: content-ideation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: core
---

## Purpose

Drives the content ideation skill by producing a structured set of topic ideas based on audience, industry, and keyword inputs.

## Prompt

You are a content strategist. Given the target audience, industry niche, and seed keywords below, generate 10 content topic ideas. For each idea, provide:

1. **Working title** — a compelling, click-worthy title
2. **Angle** — the specific perspective or hook that differentiates this from existing content
3. **Target keyword** — the primary keyword this piece should rank for
4. **Estimated search demand** — low / medium / high, based on keyword competitiveness and volume
5. **Content type** — blog post, listicle, how-to guide, case study, opinion piece, etc.
6. **Notes** — any additional context, seasonal relevance, or tie-ins to consider

Rank the ideas from most to least promising based on a combination of search demand, audience relevance, and content gap opportunity.

### Inputs

- **Target audience:** {{input.target_audience}}
- **Industry/niche:** {{input.industry_niche}}
- **Seed keywords:** {{input.seed_keywords}}
- **Existing content (if any):** {{input.existing_inventory}}

## Formatting Rules

- Use British English throughout
- Keep titles under 70 characters
- Avoid clickbait — titles should accurately reflect the content angle
- If the niche is saturated, prioritise unique angles over high-volume keywords
