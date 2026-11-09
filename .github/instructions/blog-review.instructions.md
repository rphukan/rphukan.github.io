---
description: 'Apply general editorial and reader-focused standards when reviewing or refining AI, ML, and other technical blog posts; use alongside the domain-specific AI and ML review skills.'
applyTo: 'content/posts/**/*.md'
---

# Blog Review Standards

Apply these cross-cutting standards to every blog review and refinement. They guide quality and reader experience; the AI and ML technical-review skills remain authoritative for domain-specific technical judgments.

## Reader and Purpose

- Identify the post's intended audience and what readers should understand or be able to do after reading. If this is unclear, state the assumption rather than inventing an audience.
- Check that the introduction establishes why the topic matters and what the post will cover, without promising more than the post delivers.
- Make prerequisites, scope, platform, versions, and limitations clear when they affect whether readers can follow or reproduce the material.

## Clarity and Structure

- Prefer a clear progression from problem and context through explanation, examples or implementation, results or limitations, and takeaways when those sections fit the topic. Do not force a fixed template.
- Use descriptive headings with a consistent hierarchy. Ensure each section supports the post's purpose and transitions make relationships between concepts, equations, figures, and code understandable.
- Flag genuinely dense or hard-to-scan passages, but do not infer paragraph length from Markdown source line wrapping alone.
- Define specialized terms and acronyms when the intended audience needs them; avoid both unexplained jargon and unnecessary explanations of familiar concepts.
- Prefer concise, concrete prose. Preserve the author's voice and meaningful nuance; do not treat passive voice, informal tone, or a particular style preference as an error by itself.

## Evidence and Trust

- Check that factual, comparative, performance, and outcome claims are supported by the post's evidence or appropriately qualified.
- Distinguish documented facts, observed results, estimates, opinions, and recommendations. Do not strengthen conclusions beyond the evidence or mistake an absence of detail for proof of an error.
- Flag time-sensitive claims, versions, and external references when they may mislead readers; do not claim a link or source was verified unless it was actually checked.
- Make assumptions, uncertainty, trade-offs, and relevant limitations visible where they affect the reader's interpretation.

## Examples, Code, and Visuals

- Check that examples meaningfully support the explanation and that their inputs, outputs, units, and limitations are clear where relevant.
- Keep code fences correctly tagged and examples consistent with their surrounding explanation. Identify relevant setup, dependencies, versions, platform assumptions, and data provenance; distinguish static review from executed verification.
- Flag exposed secrets, private data, or unsafe instructions in examples. Recommend placeholders and safe, portable configuration instead of reproducing sensitive values.
- Ensure figures, diagrams, tables, and captions are introduced, legible from their descriptions, and consistent with the surrounding claims. Recommend useful alternative text for informative images where appropriate.
- Check that links and referenced assets are clearly labeled and appear in context. Do not assume missing assets or broken links without verification.

## Review Findings

- Report only actionable issues that fit the assigned agent's role. Route AI/ML correctness to the technical rigor reviewer, code completeness to the code reviewer, document flow to the structural reviewer, audience issues to the audience reviewer, and sentence-level prose to the copyeditor.
- Give each finding a location, concise evidence, reader impact, and specific recommendation. Prioritize material correctness, reproducibility, and comprehension issues over optional polish.
- Separate definite defects from questions, unverifiable claims, and optional improvements. Use `PASS` when no material issue is supported in the assigned scope.
- Avoid duplicate findings across agents. Preserve disagreements that affect correctness and identify them as unresolved rather than choosing an unsupported answer.
- Keep reviews and refinements read-only: propose changes, but do not modify the source post unless the user explicitly requests edits.
