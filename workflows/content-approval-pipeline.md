---
type: workflow
id: content-approval-pipeline
title: Content Approval Pipeline
description: "Draft content, pause for human review, then revise and polish based on your feedback"
tags: [Production, Customer-Facing, Content, Gate, Approval]
connections:
  - target: content-drafting
    type: uses
  - target: draft-review
    type: uses
  - target: revision-incorporation
    type: uses
  - target: language-polish
    type: uses
  - target: consistency-check
    type: uses
  - target: llm-service
    type: runs_on
  - target: approval-workflow-guide
    type: references
metadata:
  estimated_duration: "5-15 minutes"
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "content-drafting"
  - "draft-review"
  - "revision-incorporation"
  - "language-polish"
  - "consistency-check"
execution:
  - skill: "content-drafting"
    step_type: "generation"
  - skill: "draft-review"
    step_type: "validation"
  - skill: "revision-incorporation"
    step_type: "synthesis"
  - skill: "language-polish"
    step_type: "content"
  - parallel:
    - skill: "consistency-check"
      step_type: "review"
---

## Overview

This workflow demonstrates the **gate step** pattern — a human-in-the-loop approval point where execution pauses for your review before continuing. Instead of running end-to-end on autopilot, the pipeline generates a first draft, then **stops and waits for you** to review it and provide feedback. Your feedback drives the revision, producing a final output that reflects your judgement rather than just the AI's best guess.

The gate step makes the pause intentional and valuable. You are not just rubber-stamping output — you are actively shaping the final result with specific feedback that the revision step incorporates.

The workflow uses the `llm-service` for all AI-driven stages and references the `approval-workflow-guide` asset for review guidance.

## Pipeline Stages

### Stage 1: Content Drafting (generation)

The `content-drafting` skill produces a complete first draft from your inputs: topic, target audience, content type, style guidelines, and word count. The draft is structured for easy review — clear sections with subheadings so you can give targeted feedback on specific parts.

### Stage 2: Draft Review — Gate Step (validation)

The `draft-review` skill is a **gate step**. Execution pauses and you see the draft in the Runs view with guidance on what to check. You either approve the draft or provide specific feedback describing what needs changing.

- **If you approve:** the workflow proceeds to polish, skipping revision
- **If you provide feedback:** the workflow proceeds to revision, incorporating your specific instructions

This is the core of the pipeline. Your review catches issues that automated quality checks cannot — wrong emphasis, missing context, inappropriate tone for the audience, factual errors the AI does not know about.

### Stage 3: Revision Incorporation (synthesis)

The `revision-incorporation` skill takes your feedback and produces a revised draft that addresses every point you raised. It preserves the parts that already work and makes targeted changes where you flagged issues.

### Stage 4: Language Polish (content)

The `language-polish` skill applies a final surface-level polish — spelling, grammar, punctuation, and sentence clarity. It does not change tone, restructure arguments, or rewrite content. This is the output step.

### Stage 5: Consistency Check (review, parallel)

The `consistency-check` skill runs in parallel with the polish step. It scans the document for internal consistency issues: terminology drift, tense shifts, naming inconsistencies, and internal contradictions. The report is available alongside the polished output.

## Error Handling

| Scenario | Behaviour |
|----------|-----------|
| User provides no feedback at gate | Workflow waits indefinitely — the gate step does not time out |
| User approves the draft | Revision step receives "approved" and returns the draft unchanged |
| User provides vague feedback | Revision does its best but the output quality depends on feedback specificity |
| LLM fails mid-pipeline | Pipeline halts at the failed step with an error message |

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.topic}}` | Yes | The main subject or topic to write about | "The hidden costs of technical interviews" |
| `{{input.target_audience}}` | Yes | Who this content is for | "Engineering managers and CTOs at growing startups (50-500 employees)" |
| `{{input.content_type}}` | Yes | The format to produce | "blog post" |
| `{{input.style_guidelines}}` | No | Tone, voice, and formatting preferences | "Direct and conversational. Use specific examples. Challenge assumptions." |
| `{{input.word_count}}` | No | Target word count (defaults to 1000) | "1500" |

## Outputs

| Name | Description |
|------|-------------|
| Final content | The polished, publication-ready document incorporating your feedback |
| Consistency report | Any internal consistency issues flagged by the parallel check |

## Setup

Before running this workflow:

1. Have a clear topic ready — vague topics produce vague drafts.
2. Decide on your content type and audience before starting. Changing these mid-pipeline means starting over.
3. When the gate step pauses, take your time. Read the draft carefully. The quality of the final output depends on the quality of your feedback.

## Provider Notes

- The pipeline makes 4-5 AI calls total: draft, revision, polish, and consistency check. The gate step is human-only.
- The drafting step uses temperature 0.5 for natural prose. The revision step uses 0.3 for faithful adherence to feedback.
- If you approve the draft without changes, the revision step passes the draft through unchanged — you still get the polish and consistency check.

## Example Input

To test this workflow immediately after import:

```
topic: "The hidden costs of technical interviews — why your hiring process is losing you candidates"
target_audience: "Engineering managers and CTOs at growing startups (50-500 employees)"
content_type: "blog post"
style_guidelines: "Direct and conversational. Use specific examples. Challenge assumptions."
word_count: "1500"
```
