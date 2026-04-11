---
type: prompt
id: create-content-brief
title: "Create Content Brief"
description: "Creates a structured brief for writers and content producers"
tags: [Production, Content, Planning]
inputs:
  target_audience:
    label: "Target Audience"
    description: "Who this content is for — their role, experience level, and what they care about"
    example: "Engineering managers at mid-size startups (50-200 employees)"
    required: true
    type: text
connections:
  - target: content-briefing
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the content briefing skill.

## Prompt

You are a content editor. Create a structured content brief from the topic and context below.

### Topic

{{steps.previous.output}}

### Target Audience

{{input.target_audience}}

### Instructions

Produce a content brief covering:

1. **Working title** — a clear, specific title
2. **Objective** — what this content should achieve (inform, persuade, enable)
3. **Target audience** — who reads this and what they already know
4. **Key message** — the one thing the reader should take away
5. **Outline** — section-by-section structure with key points per section
6. **Tone and voice** — formal/casual, authoritative/conversational, etc.
7. **Word count** — target length
8. **SEO targets** — primary keyword, secondary keywords (if applicable)
9. **References** — specific sources, data, or examples to include
10. **Constraints** — what to avoid, brand guidelines to follow

## Formatting Rules

- Use British English throughout
- Be specific and actionable — no vague recommendations
- Structure output clearly with headings, tables, or lists as appropriate
