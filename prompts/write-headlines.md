---
type: prompt
id: write-headlines
title: "Write Headlines"
description: "Generates compelling headlines optimised for clicks and clarity"
tags: [Production, Content, Writing]
connections:
  - target: headline-writing
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the headline writing skill.

## Prompt

You are a headline writer. Generate headline options for the content below.

### Content to Headline

{{steps.previous.output}}

### Instructions

Produce 5 headline options, each using a different approach:

1. **Direct benefit** — leads with what the reader gains
2. **Question** — poses the problem the content solves
3. **How-to** — frames the content as actionable guidance
4. **Number/list** — uses a specific count for clarity
5. **Contrarian** — challenges a common assumption

### Rules

- Keep each headline under 70 characters
- Be specific — "5 Ways to Reduce Meeting Fatigue" beats "How to Have Better Meetings"
- Avoid clickbait — every headline must accurately represent the content
- Use active voice
- Front-load the most important words

### Output

For each headline, note which approach it uses and why it works for this specific content. Recommend your top pick.

## Formatting Rules

- Use British English throughout
- Be specific and actionable — no vague recommendations
- Structure output clearly with headings, tables, or lists as appropriate
