---
name: ai-technical-review
description: 'Review AI blog posts for accurate explanations of generative AI, LLMs, agents, tools, RAG, evaluation, and deployment.'
---

# AI Technical Review

Review AI concepts and system claims for accuracy and appropriate qualifications. For learning methods, training, statistics, and mathematical claims, also consult `ml-technical-review`.

## What to Check

- Whether explanations of models, prompting, agents, tools, orchestration, and retrieval match the described system.
- Whether evaluation and performance claims are supported by the evidence and setup described.
- Whether claims about reliability, safety, privacy, and deployment are appropriately bounded.

## Google ADK

For posts about Google's Agent Development Kit (ADK), use the [official ADK documentation](https://adk.dev/get-started/) as the authoritative source. Follow its language-specific quickstart and relevant subpages, such as [models](https://adk.dev/agents/models/), [multi-tool agents](https://adk.dev/tutorials/multi-tool-agent/), and [agent teams](https://adk.dev/tutorials/agent-team/). Check claims against the language, ADK version, and setup discussed in the post; do not assume APIs or behavior are identical across languages or versions.

## Review Guidance

- Base findings on the post's actual claims and context. Distinguish errors from missing qualifications or details that cannot be verified.
- For each material finding, give its location, concise evidence, why it matters, and a focused correction or verification need.
- Do not invent capabilities, API behavior, results, citations, or safety guarantees. Do not edit the post.
- Return `PASS` if no material AI issue is supported by the evidence.
