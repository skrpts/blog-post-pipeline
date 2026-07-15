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
  - target: draft-blog-post
    type: uses
  - target: headline-writing
    type: uses
  - target: language-polish
    type: uses
  - target: seo-optimisation
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
  - "draft-blog-post"
  - "language-polish"
  - "headline-writing"
  - "seo-optimisation"
  - "content-production-checklist"
  - "brief-compliance-check"
execution:
  - skill: "content-ideation"
    step_type: "generation"
    prompt: "generate-content-ideas"
    output: { name: "ideas", type: "list" }
    context:
      source_content: "No prior analysis available — generate from the context below"
    bindings:
      content_context:
        from_input: "topic"
  - skill: "topic-selection"
    step_type: "validation"
    gate: true
    prompt: "select-topics"
    output: { name: "topic_selection", type: "text" }
  - skill: "content-briefing"
    step_type: "generation"
    prompt: "create-content-brief"
    output: { name: "brief", type: "text" }
    bindings:
      target_audience:
        from_input: "target_audience"
  - skill: "draft-blog-post"
    step_type: "generation"
    prompt: "blog-post-draft"
    output: { name: "draft", type: "text" }
    bindings:
      voice_profile:
        from_input: "style_guidelines"
      audience_profile:
        from_input: "target_audience"
      word_count:
        from_input: "word_count"
  - skill: "language-polish"
    prompt: "polish-language"
    step_type: "content"
    output: { name: "polished_post", type: "text" }
    context:
      grammar_strictness: "Professional"
    bindings:
      voice_profile:
        from_input: "style_guidelines"
      source:
        from_step: "Blog Drafting"
        field: output
  - parallel:
    - skill: "headline-writing"
      step_type: "generation"
      prompt: "write-headlines"
      output: { name: "headlines", type: "list" }
      bindings:
        source:
          from_step: "Language Polish"
          field: output
    - skill: "seo-optimisation"
      step_type: "review"
      prompt: "analyse-seo"
      output: { name: "seo_report", type: "text" }
    - skill: "brief-compliance-check"
      prompt: "check-brief-compliance"
      step_type: "review"
      output: { name: "compliance_verdict", type: "decision" }
      context:
        compliance_brief: "No specific compliance requirements"
        compliance_depth: "Standard"
      bindings:
        audience_profile:
          from_input: "target_audience"
        source:
          from_step: "Language Polish"
          field: output
---

## Overview

This workflow produces a complete, publish-ready blog post from a topic area. It generates ideas, pauses for you to pick the best ones, creates a detailed brief, writes the full draft, generates headlines, polishes the language, and runs SEO and compliance checks.

The **topic-selection** gate step is the key decision point — you review the generated ideas and choose which topics to develop. If none work, provide new direction and re-run.

## Pipeline Stages

### Stage 1: Content Ideation

**Input:** Topic (`topic`) — drives idea generation

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

Invoke the **draft-blog-post** skill via the **blog-post-draft** prompt to write the complete article. Follows the brief's structure, incorporates SEO targets, writes to your target word count (`word_count`) if set — otherwise the brief's recommendation — and applies your style guidelines and audience if provided.

**Output:** Complete blog post draft with meta description.

### Stage 5: Language Polish

**Input:** Blog post draft from Stage 4 (mapped explicitly from the draft step)

Invoke **language-polish** to clean up the article — spelling, grammar, and clarity — applying your style guidelines and grammar strictness if configured. This is the pipeline's main deliverable (`output_step`).

**Output:** Polished, publication-ready blog post.

### Stage 6: Headlines & Quality Checks (Parallel)

Three agents run simultaneously, each mapped explicitly to the **polished post** from Stage 5:
- **Headline Writing** — generates headline options via **write-headlines**
- **SEO Optimisation** — evaluates on-page SEO and keyword usage via **analyse-seo**
- **Brief Compliance** — verifies the post meets the original brief's requirements via **check-brief-compliance**

**Output:** Headline options and review reports (supplementary — do not gate the main output).

## Error Handling

- If ideation produces no viable topics, the gate step lets you redirect with new input
- If the draft deviates from the brief, the compliance check flags it
- If SEO and editorial recommendations conflict, editorial quality takes priority

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.topic}}` | Yes | Topic area or niche | `AI tools for B2B marketing teams` |
| `{{input.target_audience}}` | No | Who the post is for | `Marketing managers at mid-size SaaS companies` |
| `{{input.style_guidelines}}` | No | Voice and tone to write in | `Warm, plain-spoken, second person; short sentences` |
| `{{input.word_count}}` | No | Desired length in words. Defaults to the brief's recommendation | `1500` |

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
3. **Prepare your inputs** — a topic is required. Optionally supply a target audience, style guidelines, and a target word count; each refines the output but has a sensible default.

## Provider Notes

- The editorial review and drafting steps benefit from a model with strong writing and grammar capabilities.
- SEO optimisation is a structured analytical task — most models handle it well.
- Content ideation benefits from a model with broad knowledge and creative generation.
- The full pipeline uses moderate token counts — no long-context requirements.

## Example Input

To test this workflow immediately after import:

```
Topic: "Local SEO for small service businesses (plumbers, electricians, landscapers)"
Target audience: "Small business owners who are new to content marketing"
Style guidelines: "Warm, plain-spoken, second person; short sentences"
Word count: 1200
```
