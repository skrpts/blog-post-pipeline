---
type: prompt
id: select-topics
title: "Select Topics"
description: "Gate prompt — pauses for user to select topics from the generated ideas"
tags: [Production, Gate, Content]
connections:
  - target: topic-selection
    type: derived_from
metadata:
  output_format: text
  prompt_type: gate
---

## Topic Selection

Review the topic ideas below and tell us which ones to develop into blog posts.

### Generated Topics

{{steps.previous.output}}

### How to respond

- **Select topics:** Tell us which ones you want (by number, title, or description). You can pick one topic for a single focused post, or multiple topics for a series.
- **Reject all:** If none of these work, describe what you're looking for instead and re-run the workflow with updated input. For example: "None of these hit the mark — I need topics about [specific area]."

### Examples

- "Develop topic 2 — the pricing model one"
- "I want topics 1, 3, and 5 — all three as separate posts"
- "Topic 4, but angle it more toward engineering managers not just engineers"
- "None of these — I need topics about developer onboarding, not pricing"

{{steps.previous.output}}
