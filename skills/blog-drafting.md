---
type: skill
id: blog-drafting
title: Blog Drafting
description: "Writes a complete blog post from a content brief — the core generation step"
tags: [Production, Content, Writing]
connections:
  - target: llm-service
    type: runs_on
context_params:
  voice_profile:
    label: "Voice Profile"
    description: "Creator's writing style for personalised drafting"
    required: false
  audience_profile:
    label: "Audience Profile"
    description: "Target audience for tone and depth calibration"
    required: false
---

## Capability

Takes a content brief and produces a complete, publication-ready blog post. Follows the brief's structure, tone guidance, SEO targets, and word count requirements.

## When to Use

- After content briefing has produced a structured brief
- As the main generation step in a blog production pipeline

## What It Does

1. **Structure** — follows the outline in the brief (H2/H3 headings, section order)
2. **Tone** — matches the voice and style guidance
3. **SEO** — incorporates target keywords naturally
4. **Length** — hits the specified word count
5. **Engagement** — opens with a hook, uses concrete examples, ends with CTA
6. **Formatting** — short paragraphs, bullet points, bold key terms
