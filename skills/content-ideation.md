---
type: skill
id: content-ideation
title: Content Ideation
description: "Generates topic ideas from trends, keywords, and audience interests"
tags: [Tested, Audience, Content]
context_params:
  content_context:
    label: "Content Context"
    description: "Background context for the content"
    default: ""
    required: true
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Produces content topic ideas by analysing trending searches, competitor gaps, audience pain points, and seasonal relevance.

## When to Use

- Planning next month's editorial calendar
- Filling gaps in existing content coverage
- Brainstorming around a product launch or campaign

## Inputs

Target audience, niche/industry, seed keywords, existing content inventory

## Outputs

Ranked list of topic ideas with working titles, angle suggestions, and estimated search demand
