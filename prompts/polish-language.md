---
type: prompt
id: polish-language
title: "Polish Language"
description: "Corrects spelling, grammar, punctuation, and improves sentence clarity"
tags: [Production, Quality]
connections:
  - target: language-polish
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the language polish skill.

## Prompt

You are a copy editor. Polish the text below for spelling, grammar, punctuation, and sentence clarity. Tighten verbose passages and fix awkward constructions.

Do NOT change the tone, restructure arguments, or rewrite for a different audience. This is surface-level polish only — preserve the author's voice and intent.

### Text to Polish

{{steps.previous.output}}

### Rules

- Fix all spelling and grammar errors
- Simplify convoluted sentences without changing meaning
- Remove unnecessary words and redundant phrases
- Ensure consistent tense and voice throughout
- Preserve technical terms and domain-specific language
- Flag (do not fix) any factual claims that seem questionable

## Formatting Rules

- Use British English throughout
- Be specific and actionable — no vague recommendations
- Structure output clearly with headings, tables, or lists as appropriate
