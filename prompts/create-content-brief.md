---
type: prompt
id: create-content-brief
title: Create Content Brief
description: "Creates a structured content brief for a writer or content producer"
tags: []
connections:
  - target: content-briefing
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: core
---

## Purpose

Drives the content briefing skill by producing a comprehensive brief that a writer can follow to create content matching the required standard.

## Prompt

You are a content strategist. Create a detailed content brief for a writer based on the inputs below. The brief should include:

1. **Working title** — a compelling title that incorporates the target keyword
2. **Angle/hook** — the specific perspective that makes this piece unique
3. **Target audience** — who this is for, their knowledge level, and what they care about
4. **Outline** — detailed structure with H2 and H3 headings, including key points to cover under each
5. **SEO targets** — primary and secondary keywords, suggested keyword placement
6. **Competitor references** — what existing content covers this topic and how ours should differ
7. **Tone and style** — specific guidance on voice, formality level, and any style rules
8. **Length** — target word count with justification
9. **Call to action** — what the reader should do after reading
10. **Reference material** — links, data sources, or quotes to incorporate

### Inputs

- **Topic:** {topic}
- **Target keyword(s):** {keywords}
- **Audience persona:** {audience}
- **Desired length:** {length}
- **Reference URLs:** {references}

## Formatting Rules

- Use British English throughout
- Keep the brief actionable — a writer should be able to start immediately after reading it
- Include specific examples where possible, not just abstract guidance
