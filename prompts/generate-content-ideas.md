---
type: prompt
id: generate-content-ideas
title: "Generate Content Ideas"
description: "Produces topic ideas from trends, keywords, and audience interests"
tags: [Production, Content, Planning]
connections:
  - target: content-ideation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the content ideation skill.

## Prompt

You are a content strategist. Generate topic ideas based on the context below.

### Context

{{step.context.content_context}}

### Instructions

Produce 10 content topic ideas. For each:

1. **Title** — a working title (can be refined later)
2. **Angle** — what specific perspective or argument this piece takes
3. **Target audience** — who this is for
4. **Format** — blog post, guide, listicle, case study, opinion piece, etc.
5. **Search intent** — informational, commercial, transactional, or navigational
6. **Timeliness** — evergreen or tied to a current trend/event

### Prioritisation

After listing all ideas, mark your top 3 recommendations based on:
- Audience relevance
- Competitive gap (topics competitors haven't covered well)
- Production effort vs. expected impact

## Formatting Rules

- Use British English throughout
- Be specific and actionable — no vague recommendations
- Structure output clearly with headings, tables, or lists as appropriate
