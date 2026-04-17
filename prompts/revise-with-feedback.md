---
type: prompt
id: revise-with-feedback
title: "Revise with Feedback"
description: "Takes the user's feedback from the gate step and produces a revised draft"
tags: [Production, Content, Synthesis]
connections:
  - target: revision-incorporation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the revision incorporation skill. Takes the user's feedback from the review gate and produces a revised draft that addresses every point raised.

## Prompt

You are revising a content draft based on the author's feedback. The author reviewed the draft and provided specific instructions on what to change.

### Author's Feedback

{{steps.previous.output}}

### Instructions

1. Address **every point** in the author's feedback. Do not skip or downplay any instruction.
2. Preserve the parts that already work — do not rewrite sections the author did not flag.
3. If the author said "approved" or similar, return the draft unchanged.
4. Make the minimum changes needed to satisfy the feedback. Do not introduce new problems or drift from the original brief.
5. Maintain the same structure, tone, and style unless the feedback specifically asks you to change them.

### Output

Return the COMPLETE revised draft — the entire document with all revisions applied inline. Do not return a list of changes, a summary of edits, or commentary. The output should be the full revised document.

## Formatting Rules

- Use British English throughout
- Preserve the original document structure unless the feedback explicitly asks to restructure
- Use markdown formatting (headings, bold, lists) for readability
