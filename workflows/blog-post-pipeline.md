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
  - target: anthropic-claude
    type: runs_on
  - target: openai-gpt4
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
