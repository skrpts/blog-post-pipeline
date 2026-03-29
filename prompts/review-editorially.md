---
type: prompt
id: review-editorially
title: Review Editorially
description: "Reviews content for grammar, style, and brand voice compliance"
tags: [Production, Communication, Content]
connections:
  - target: editorial-review
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: core
---

## Purpose

Drives the editorial review skill by checking content against style guides and brand voice standards.

## Prompt

You are a senior editor. Review the following content against the style guide provided. Evaluate:

1. **Grammar and spelling** — flag any errors, using British English conventions
2. **Style guide compliance** — check adherence to the provided style guide rules (terminology, formatting, capitalisation)
3. **Brand voice** — does the tone match the brand voice description? Flag any sections that drift
4. **Consistency** — are terms, capitalisation, and formatting consistent throughout?
5. **Clarity** — flag any ambiguous sentences, jargon without explanation, or unnecessarily complex phrasing
6. **Structure** — is the piece well-organised with clear transitions between sections?

For each issue found, provide:
- The original text
- The suggested revision
- The reason for the change (grammar rule, style guide reference, or voice guidance)

Conclude with a revised version of the full content incorporating all corrections.

### Inputs

- **Draft content:** {{steps.blog-post-draft.output}}
- **Style guide:** Use the editorial style guide from the sources
- **Brand voice description:** Use the brand voice guide from the sources

## Formatting Rules

- Use British English throughout
- Be constructive — explain why changes improve the piece
- Categorise issues as: error (must fix), recommendation (should fix), suggestion (could improve)
