---
name: ml-technical-review
description: 'Review Machine Learning blog posts for accuracy in data, learning methods, model objectives, optimization, evaluation, and mathematical claims.'
---

# Machine Learning Technical Review

Review Machine Learning claims for correctness and appropriate qualifications. For AI system and application claims, also consult `ai-technical-review`.

## What to Check

- Whether the method, objective, data, and evaluation fit the problem being described.
- Whether equations, assumptions, terminology, and tensor dimensions are internally consistent.
- Whether data preparation or evaluation could introduce leakage or support an overstated conclusion.
- Whether claims about performance, convergence, or generalization are supported and appropriately qualified.

## Review Guidance

- Use [Dive into Deep Learning](https://d2l.ai/chapter_preliminaries/index.html) and its relevant chapters as an authoritative reference for deep-learning concepts.
- Ground findings in the post's actual claims and context. Distinguish clear errors from missing assumptions, limitations, or claims that cannot be verified.
- For each material finding, give its location, concise evidence, why it matters, and a focused correction or verification need.
- Do not invent results, proofs, citations, or implementation behavior. Do not edit the post.
- Return `PASS` if no material ML issue is supported by the evidence.
