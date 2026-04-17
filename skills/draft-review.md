---
type: skill
id: draft-review
title: Draft Review
description: "Human gate — pauses execution for the user to review a draft and provide feedback or approval"
tags: [Production, Gate, Review]
connections:
  - target: llm-service
    type: runs_on
metadata:
  gate: true
---

## Capability

Pauses the workflow and presents the generated draft to the user for review. The user either approves the draft or provides specific feedback describing what needs changing. The user's response becomes this step's output, which the revision step uses to produce an improved version.

This is a **gate step** — execution pauses until the user responds. This pause is intentional: human judgement at the draft stage catches issues that automated review cannot, and the user's specific feedback produces far better revisions than generic quality criteria.

## When to Use

- After a drafting step produces content that needs human sign-off
- When the quality bar requires human judgement, not just automated checks
- In any pipeline where the user's specific feedback is more valuable than another AI pass

## What Happens

1. Execution pauses with status `awaiting_input`
2. The user sees the draft in the Runs view with review guidance
3. The user reviews the draft and responds:
   - **"approved"** or similar affirmation — workflow proceeds to polish
   - **Specific feedback** — workflow proceeds to revision, incorporating the feedback
4. The user's response becomes this step's output

## Review Guidance

The prompt guides the user on what to check:

- Does the draft address the topic thoroughly?
- Is it pitched at the right level for the target audience?
- Is the structure logical and easy to follow?
- Are there any factual errors or unsupported claims?
- Does the tone match the style guidelines?
- What specific sections need improvement, and how?
