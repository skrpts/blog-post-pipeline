---
type: workflow
id: blog-post-pipeline
title: Blog Post Pipeline
description: "End-to-end blog production: ideation, briefing, draft, editorial review, and SEO optimisation"
tags: [Production, Customer-Facing, Content, Optimisation, Review]
connections:
  - target: content-ideation
    type: uses
  - target: topic-selection
    type: uses
  - target: content-briefing
    type: uses
  - target: blog-drafting
    type: uses
  - target: headline-writing
    type: uses
  - target: language-polish
    type: uses
  - target: seo-optimisation
    type: uses
  - target: content-production-checklist
    type: uses
  - target: brief-compliance-check
    type: uses
  - target: llm-service
    type: runs_on
  - target: analyse-seo
    type: references
metadata:
  estimated_duration: "10-20 minutes"
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "content-ideation"
  - "topic-selection"
  - "content-briefing"
  - "blog-drafting"
  - "headline-writing"
  - "language-polish"
  - "seo-optimisation"
  - "content-production-checklist"
  - "brief-compliance-check"
execution:
  - skill: "content-ideation"
    step_type: "generation"
    prompt: "generate-content-ideas"
    context:
      content_context: ""
  - skill: "topic-selection"
    step_type: "validation"
    prompt: "select-topics"
  - skill: "content-briefing"
    step_type: "generation"
    prompt: "create-content-brief"
    context:
      target_audience: ""
  - skill: "blog-drafting"
    step_type: "generation"
    prompt: "blog-post-draft"
  - skill: "headline-writing"
    step_type: "generation"
    prompt: "write-headlines"
  - skill: "language-polish"
    step_type: "content"
  - parallel:
    - skill: "seo-optimisation"
      step_type: "review"
      prompt: "analyse-seo"
    - skill: "content-production-checklist"
      step_type: "review"
    - skill: "brief-compliance-check"
      step_type: "review"
---

## Overview

This workflow produces a complete, publish-ready blog post from a topic area. It generates ideas, pauses for you to pick the best ones, creates a detailed brief, writes the full draft, generates headlines, polishes the language, and runs SEO and compliance checks.

The **topic-selection** gate step is the key decision point — you review the generated ideas and choose which topics to develop. If none work, provide new direction and re-run.

## Pipeline Stages

### Stage 1: Content Ideation

**Input:** Topic/niche, target audience

Invoke the **content-ideation** skill via the **generate-content-ideas** prompt to produce 10 ranked topic ideas with titles, angles, formats, and search intent.

**Output:** Ranked list of topic ideas.

### Stage 2: Topic Selection (Gate Step)

Execution **pauses** via the **topic-selection** gate step. You review the generated ideas and respond:

- **Select topics** — pick one or more topics to develop (by number or description)
- **Reject all** — if none work, describe what you need instead and re-run with new input

Your selection becomes the input for the content briefing step.

**Output:** Your topic selection and any additional direction.

### Stage 3: Content Briefing

**Input:** Selected topic(s) from Stage 2

Invoke the **content-briefing** skill via the **create-content-brief** prompt to produce a structured brief: outline, SEO targets, tone guidance, word count, and CTA.

**Output:** Detailed content brief.

### Stage 4: Blog Post Draft

**Input:** Content brief from Stage 3

Invoke the **blog-drafting** skill via the **blog-post-draft** prompt to write the complete article. Follows the brief's structure, incorporates SEO targets, and applies your Voice Profile if set.

**Output:** Complete blog post draft with meta description.

### Stage 5: Headline Writing

**Input:** Blog post draft from Stage 4

Invoke the **headline-writing** skill via the **write-headlines** prompt to generate headline options for the draft.

**Output:** 5 headline options with rationale.

### Stage 6: Language Polish

Invoke **language-polish** to clean up the final post. Applies your Voice Profile and grammar strictness settings if configured.

**Output:** Polished, publication-ready blog post.

### Stage 7: Quality Checks (Parallel)

Three review agents run simultaneously:
- **SEO Optimisation** — evaluates on-page SEO and keyword usage via **analyse-seo**
- **Content Production Checklist** — checks against production quality criteria
- **Brief Compliance** — verifies the post meets the original brief's requirements

**Output:** Review reports (supplementary — do not gate the main output).

## Error Handling

- If ideation produces no viable topics, the gate step lets you redirect with new input
- If the draft deviates from the brief, the compliance check flags it
- If SEO and editorial recommendations conflict, editorial quality takes priority

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.topic}}` | Yes | Topic area or niche | `AI tools for B2B marketing teams` |
| `{{input.target_audience}}` | Yes | Who the post is for | `Marketing managers at mid-size SaaS companies` |
| `{{input.target_length}}` | No | Desired word count. Default: 1500 | `2000` |

## Outputs

| Name | Description |
|------|-------------|
| Blog post | Publish-ready article in markdown with headings, body text, and conclusion |
| Meta data | SEO title, meta description, target keywords, and suggested slug |
| SEO score | Numeric score (0-100) with breakdown of on-page SEO factors |

## Setup

Before running this workflow:

1. **No external services required** — this workflow runs entirely on your configured LLM provider.
2. **Customise the style guides** — review the three source documents (`brand-voice-guide`, `editorial-style-guide`, `seo-guidelines`) and update them to match your brand and editorial standards.
3. **Prepare your inputs** — you'll need a target audience, industry niche, and seed keywords at minimum.

## Provider Notes

- The editorial review and drafting steps benefit from a model with strong writing and grammar capabilities.
- SEO optimisation is a structured analytical task — most models handle it well.
- Content ideation benefits from a model with broad knowledge and creative generation.
- The full pipeline uses moderate token counts — no long-context requirements.

## Example Input

To test this workflow immediately after import:

```
Target audience: "Small business owners who are new to content marketing"
Industry niche: "Local service businesses (plumbers, electricians, landscapers)"
Seed keywords: "local SEO, Google Business Profile, customer reviews"
Target length: 1200
```
