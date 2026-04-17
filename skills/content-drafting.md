---
type: skill
id: content-drafting
title: Content Drafting
description: "Generates a first draft from a topic brief, audience, content type, and style inputs"
tags: [Production, Content, Writing]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Produces a complete first draft of any content type — blog post, proposal, report, newsletter, or similar — from a structured brief. Takes the topic, target audience, content type, style guidelines, and word count, then generates a well-structured draft ready for human review.

This is a first-draft skill. It prioritises getting the structure, arguments, and tone right rather than surface-level polish. The expectation is that a human will review and provide feedback before the draft is finalised.

## When to Use

- At the start of any content pipeline where human approval matters
- When you need a structured first draft that a reviewer can meaningfully critique
- Before a gate step where a human will provide specific feedback

## Inputs

- Topic or subject brief
- Target audience description
- Content type (e.g. blog post, proposal, report)
- Style guidelines (optional — sensible defaults apply)
- Target word count (optional — defaults to 1000)

## Outputs

A complete first draft with title, introduction, body sections with subheadings, and conclusion. Structured for easy review — each section is clearly delineated so the reviewer can give targeted feedback.
