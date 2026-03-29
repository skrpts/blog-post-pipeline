---
type: skill
id: seo-optimisation
title: SEO Optimisation
description: "Analyses and improves content for search engine visibility"
tags: [Production, Content, Optimisation]
connections:
  - target: llm-service
    type: runs_on
  - target: seo-guidelines
    type: references
---

## Capability

Evaluates content against on-page SEO best practices: keyword placement, heading structure, internal linking opportunities, readability, and meta data quality.

## When to Use

- Before publishing any blog post or landing page
- Auditing existing content for ranking improvements
- Comparing content against top-ranking competitors

## Inputs

Draft content + target keyword(s) + competitor URLs (optional)

## Outputs

SEO score with actionable recommendations: keyword density, missing headings, suggested internal links, meta description draft
