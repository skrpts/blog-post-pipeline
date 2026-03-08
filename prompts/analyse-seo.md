---
type: prompt
id: analyse-seo
title: Analyse SEO
description: "Analyses content against target keywords for search engine optimisation"
tags: []
connections:
  - target: seo-optimisation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: core
---

## Purpose

Drives the SEO optimisation skill by evaluating draft content against on-page SEO best practices.

## Prompt

You are an SEO specialist. Analyse the following content against the target keyword. Evaluate:

1. **Keyword placement** — is the target keyword in the title, first paragraph, at least one H2, and the meta description?
2. **Heading structure** — is there a logical H1 > H2 > H3 hierarchy? Are headings descriptive and keyword-relevant?
3. **Keyword density** — is the target keyword used naturally throughout, without stuffing? Aim for 1-2% density.
4. **Internal linking** — are there opportunities to link to related content? Suggest specific anchor text and target pages.
5. **Readability** — is the content scannable? Short paragraphs, bullet points, clear transitions?
6. **Meta data** — draft a meta title (under 60 characters) and meta description (under 155 characters).
7. **Content length** — is the piece long enough to compete for the target keyword? Compare to estimated competitor word counts.

Provide an overall SEO score out of 100 and a prioritised list of improvements.

### Inputs

- **Draft content:** {content}
- **Target keyword(s):** {keywords}
- **Competitor URLs (optional):** {competitors}

## Formatting Rules

- Use British English throughout
- Be specific — "add the keyword to H2" is better than "improve keyword usage"
- Distinguish between critical issues (blocking publication) and nice-to-haves
