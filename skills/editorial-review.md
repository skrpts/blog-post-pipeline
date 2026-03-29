---
type: skill
id: editorial-review
title: Editorial Review
description: "Checks grammar, style consistency, and brand voice alignment"
tags: [Tested, Communication, Content, Review]
connections:
  - target: llm-service
    type: runs_on
  - target: brand-voice-guide
    type: references
  - target: editorial-style-guide
    type: references
---

## Capability

Reviews content for grammatical correctness, adherence to a style guide, consistent terminology, and brand voice alignment.

## When to Use

- Final review before publishing
- Onboarding new writers to ensure consistency
- Auditing existing content for style drift

## Inputs

Draft content + style guide + brand voice description

## Outputs

Annotated corrections, style violations, tone mismatches, and a revised version matching brand standards
