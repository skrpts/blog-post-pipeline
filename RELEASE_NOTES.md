# Release Notes

## v1.2.21
GH#844 — migrate the gate step from node-meta (`metadata.gate: true` in the skill) to the canonical execution-entry `gate: true` on the workflow step. Single source of truth; the engine + app read the execution entry. No behaviour change — `IsGate` is identical.

## v1.2.20
GH#781 / K-045 — fix the pipeline tail data-flow and repin dependencies. The tail chained on positional `{{steps.previous.output}}`, so with headline-writing sitting between draft and polish, language-polish (and SEO/compliance) operated on the HEADLINES, not the article. Reordered to draft -> language-polish -> parallel[headline-writing, seo, compliance] and mapped each steps source EXPLICITLY: language-polish source from the draft; headline-writing / brief-compliance-check source from the polished post (via `from_step`); analyse-seo already referenced the polished output explicitly. The three shared tail prompts now expose a `source` slot (see their notes). Also repinned the `dependencies:` lock to the current published dep versions (closing a K-038 propagation gap where the lock trailed at 1.0.1). A supplied topic now flows to a polished ARTICLE at output_step.

## v1.2.19
GH#775 follow-up — restore `word_count` as a real, functional input. v1.2.18 dropped it (the app stopped offering it) on the assumption that binding it needed the shared `create-content-brief` prompt (K-038). That premise was wrong: it wires cleanly into the **local** `blog-post-draft` prompt. Declared `word_count` (optional) and bound it into the draft step — the draft now honours a supplied target length (falling back to the brief's recommendation when omitted). Also reconciled the whole skrpt's documentation with the actual inputs (topic required; target_audience/style_guidelines/word_count optional): the Inputs table, the stage descriptions, the Setup notes, and the Example Input block — clearing the earlier drift where the docs advertised inputs (industry niche, seed keywords, target length) that were never wired.

## v1.2.18
GH#775 — the pipeline never actually accepted a topic. Its inputs lived only in the prose Inputs table, never structurally declared where the engine reads them (a prompt `inputs:` block), so every step ran on static placeholders ("No subject supplied", "General professional audience"). Declared `topic` (required) plus optional `target_audience` and `style_guidelines`, then bound them into the step contexts they feed: content-ideation `content_context` ← `topic` (the first step, so a supplied topic drives ideation), content-briefing `target_audience` ← `target_audience`, draft-blog-post `voice_profile` ← `style_guidelines` / `audience_profile` ← `target_audience`, language-polish `voice_profile` ← `style_guidelines`, brief-compliance-check `audience_profile` ← `target_audience`. A supplied topic, audience, and style now flow through the whole pipeline. (`word_count`/length remains a deliberate deferral — binding it needs a shared-prompt change; it degrades to the default.)

## v1.2.17
GH#745 — declare per-step `output: {name, type}` on every execution step (`ideas`/list, `topic_selection`/text, `brief`/text, `draft`/text, `headlines`/list, `polished_post`/text, `seo_report`/text, `compliance_verdict`/decision). Lights up the #744 rich flow-map — steps now show named, typed outputs instead of the step-attributed fallback. Content-only; no bindings or logic changes.

## v1.2.16
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 15 inline shared-content files and declare 15 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Internal slug references rewritten for E2 rename/mirror-drop pair(s): blog-drafting→draft-blog-post. Closes pre-Step-3 inline-vendoring for this bundle.

## v1.2.15
Wave 2: re-signed with canonical engine signing pipeline.

## v1.2.14
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.2.13
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.2.12
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.2.11
Initial catalogue release with full structural and content-quality validation. All scanner checks pass.
