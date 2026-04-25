---
type: prompt
id: blog-post-draft
title: Blog Post Draft
description: "Writes a complete blog post from a content brief"
tags: [Customer-Facing, Content, Optimisation]
connections:
  - target: blog-drafting
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Produces a full blog post draft following the structure, tone, and SEO targets specified in a content brief.

## Voice Profile

{{step.context.voice_profile}}

If a voice profile is provided above, write in the creator's voice — match their sentence patterns, vocabulary, and rhetorical devices. If not, write in a clear, engaging style.

## Audience Profile

{{step.context.audience_profile}}

If an audience profile is provided, calibrate tone, depth, and examples for this audience.

## Prompt

You are an experienced content writer. Using the content brief below, write a complete blog post. Follow these guidelines:

1. **Structure** — follow the outline in the brief exactly, using the specified H2 and H3 headings
2. **Tone** — match the tone and style guidance in the brief
3. **SEO** — incorporate the target keyword naturally in the title, first paragraph, at least two H2 headings, and the conclusion. Aim for 1-2% keyword density without stuffing.
4. **Length** — hit the target word count specified in the brief
5. **Engagement** — open with a hook that addresses the reader's pain point or curiosity. Use examples, data, and analogies to make abstract points concrete.
6. **Call to action** — end with the CTA specified in the brief
7. **Formatting** — use short paragraphs (3-4 sentences max), bullet points for lists, and bold for key terms on first use

### Inputs

- **Content brief:** {{steps.previous.output}}

## Formatting Rules

- Use British English throughout
- Write in second person ("you") unless the brief specifies otherwise
- Avoid filler phrases ("In today's world", "It's no secret that", "At the end of the day")
- Every paragraph should advance the argument or provide new information
- Include a meta description (under 155 characters) at the end of the draft
