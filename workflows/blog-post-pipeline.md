---
type: workflow
id: blog-post-pipeline
title: Blog Post Pipeline
description: "End-to-end blog production: ideation, briefing, draft, editorial review, and SEO optimisation"
tags: [Production, Customer-Facing]
connections:
  - target: content-ideation
    type: uses
  - target: content-briefing
    type: uses
  - target: blog-post-draft
    type: uses
  - target: editorial-review
    type: uses
  - target: seo-optimisation
    type: uses
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "5-15 minutes"
  trigger: manual
---

## Overview

This workflow orchestrates the complete blog post production process, from initial ideation through to a publish-ready, SEO-optimised article. Each stage builds on the output of the previous one, with quality gates at the editorial and SEO review stages.

## Pipeline Stages

### Stage 1: Content Ideation

**Input:** Target audience, industry niche, seed keywords, existing content inventory

Invoke the **content-ideation** skill to generate a ranked list of topic ideas. The content strategist or editor selects the best topic from the list and confirms the angle.

**Output:** Selected topic with working title and angle.

### Stage 2: Content Briefing

**Input:** Selected topic, target keywords, audience persona, desired length, reference URLs

Invoke the **create-content-brief** prompt to produce a detailed brief covering outline, SEO targets, tone guidance, and reference material.

**Output:** Structured content brief ready for a writer.

### Stage 3: Blog Post Draft

**Input:** Content brief from Stage 2

Invoke the **blog-post-draft** prompt to write the full article following the brief's structure, tone, and SEO targets.

**Output:** Complete blog post draft.

### Stage 4: Editorial Review

**Input:** Draft from Stage 3 + brand voice guide + editorial style guide

Invoke the **editorial-review** skill to check grammar, style compliance, and brand voice alignment. The skill produces annotated corrections and a revised version.

**Gate:** All errors must be resolved before proceeding. Recommendations should be addressed; suggestions are optional.

**Output:** Editorially reviewed and revised draft.

### Stage 5: SEO Optimisation

**Input:** Reviewed draft from Stage 4 + target keywords

Invoke the **seo-optimisation** skill to evaluate on-page SEO and produce actionable recommendations. Apply the recommendations to produce the final version.

**Gate:** SEO score must be 70 or above before publishing.

**Output:** Publish-ready blog post with meta data.

## Error Handling

- If ideation produces no viable topics, expand the seed keywords or broaden the niche
- If the draft significantly deviates from the brief, return to Stage 3 rather than trying to fix in review
- If SEO and editorial recommendations conflict (e.g., keyword placement vs. natural prose), editorial quality takes priority

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.target_audience}}` | Yes | Who the post is written for | "SaaS founders and product managers" |
| `{{input.industry_niche}}` | Yes | The topic area or industry | "B2B product-led growth" |
| `{{input.seed_keywords}}` | Yes | Initial keywords to guide ideation | "onboarding, activation, product-led growth" |
| `{{input.existing_inventory}}` | No | Titles of existing blog posts to avoid duplication | "5 Onboarding Mistakes, PLG Playbook" |
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
