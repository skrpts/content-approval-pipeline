---
type: skill
id: revision-incorporation
title: Revision Incorporation
description: "Takes a draft and the user's feedback, then produces a revised version addressing every point raised"
tags: [Production, Content, Synthesis]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Receives the original draft and the user's specific feedback from the gate step, then produces a revised version that addresses every point raised. Preserves the parts that already work while improving the areas the user flagged.

This is not a rewrite — it is a targeted revision. The skill treats the user's feedback as authoritative and makes the minimum changes needed to satisfy it, without introducing new problems or losing what was already good.

## When to Use

- After a gate step where the user has provided specific feedback on a draft
- When the revision needs to be faithful to the user's intent, not just generically improved
- In any pipeline where human feedback drives the next version

## Inputs

- The original draft (from the drafting step)
- The user's feedback (from the gate step)

## Outputs

A revised draft that addresses each point in the user's feedback. Changes are incorporated inline — the output is a complete, revised document, not a list of changes.
