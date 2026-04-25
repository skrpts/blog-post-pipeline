---
type: skill
id: topic-selection
title: Topic Selection
description: "Human gate — pauses for the user to select topics from the generated ideas"
tags: [Production, Gate, Content]
connections:
  - target: llm-service
    type: runs_on
metadata:
  gate: true
---

## Capability

Pauses the workflow and presents the generated topic ideas to the user. The user selects one or more topics to develop into blog posts, or rejects all topics and provides new direction.

This is a **gate step** — execution pauses until the user responds.

## What Happens

1. Execution pauses with status `awaiting_input`
2. The user sees the topic ideas from the ideation step
3. The user responds with:
   - **Selected topics** — "topics 1, 3, and 5" or "I want the pricing model one"
   - **Rejection** — "none of these work, try topics about X instead" → user should re-run with new input
4. The user's selection becomes this step's output, feeding into the content briefing step
