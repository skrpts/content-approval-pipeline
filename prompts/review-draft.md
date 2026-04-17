---
type: prompt
id: review-draft
title: "Review Draft"
description: "Gate prompt — shown to the user when execution pauses for draft review"
tags: [Production, Gate, Review]
connections:
  - target: draft-review
    type: derived_from
metadata:
  output_format: text
  prompt_type: gate
---

## Your Draft Is Ready for Review

Please review the draft below. This is your chance to shape the final output — your feedback drives the next revision.

### What to check

- **Topic coverage** — Does the draft address the subject thoroughly? Is anything important missing?
- **Audience fit** — Is it pitched at the right level? Will your target readers find it relevant and useful?
- **Structure** — Is the flow logical? Do the sections build on each other?
- **Tone** — Does it match the style you asked for? Too formal? Too casual? Too generic?
- **Arguments** — Are the claims supported? Are there unsupported assertions that need evidence?
- **Specific sections** — Is any section notably weak, off-topic, or redundant?

### How to respond

- **If the draft is good as-is:** respond with "approved" or "looks good"
- **If changes are needed:** describe what needs changing — be specific. "The opening is too generic — lead with the cost statistic instead" is far more useful than "make it better"

The more specific your feedback, the better the revision.

---

{{steps.previous.output}}
