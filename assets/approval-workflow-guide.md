---
type: asset
id: approval-workflow-guide
title: Approval Workflow Guide
description: "Guide explaining how the content approval workflow works and what to look for during review"
tags: [Production, Documentation]
connections: []
---

## How the Content Approval Pipeline Works

This workflow generates a content draft, then **pauses for your review** before continuing. Your feedback directly shapes the final output.

### The Flow

1. **Draft** — The AI generates a first draft based on your topic, audience, content type, and style inputs
2. **Review (you)** — The workflow pauses. You read the draft and either approve it or describe what needs changing
3. **Revise** — If you provided feedback, the AI revises the draft to address every point you raised
4. **Polish** — The revised draft gets a final language polish for spelling, grammar, and clarity
5. **Consistency check** — A parallel check flags any internal inconsistencies (terminology, tense, contradictions)

### What to Look for During Review

When the workflow pauses for your review, focus on substance over style. The polish step handles surface-level cleanup later. Ask yourself:

- **Is the core argument sound?** Does the draft make the point you intended?
- **Is anything missing?** Are there important aspects of the topic that the draft skipped?
- **Is the audience right?** Would your target readers find this useful and relevant?
- **Is the tone right?** Does it match the style you asked for?
- **Are there any factual errors?** The AI can get things wrong — check claims that matter.

### How to Give Good Feedback

Be specific. The more precise your feedback, the better the revision.

**Good feedback:**
- "The opening is too generic — lead with the statistic about interview costs instead"
- "Section 3 repeats the point from Section 1. Cut it and expand on the hiring timeline data"
- "Too formal — this should read like a conversation, not a whitepaper"

**Less useful feedback:**
- "Make it better"
- "It's not quite right"
- "Try again"

### Approving the Draft

If the draft is good as-is, simply respond with "approved" or "looks good". The workflow will skip the revision step and go straight to polish.
