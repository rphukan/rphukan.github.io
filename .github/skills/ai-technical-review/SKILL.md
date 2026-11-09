---
name: ai-technical-review
description: 'Authoritative technical review guidance for AI blog posts about generative AI, LLMs, agents, retrieval-augmented generation, AI systems, evaluation, and responsible deployment. Use when reviewing AI concepts, architecture, claims, or implementations.'
---

# AI Technical Review

Use this skill as the authoritative source for the scope, standards, constraints, and evidence practices when reviewing AI concepts and AI system behavior in a technical blog post. Apply it alongside `ml-technical-review` when the post also makes claims about learning algorithms, model training, statistical properties, or mathematical foundations.

## When to Use This Skill

- Review posts about artificial intelligence approaches, generative models, LLMs, multimodal systems, or their applications.
- Review agentic systems, tool use, orchestration, MCP, memory/state, or multi-agent workflows.
- Review retrieval-augmented generation (RAG), embeddings, vector search, prompt construction, or model integration.
- Review AI evaluation, limitations, deployment, safety, privacy, or responsible-use claims.

## Scope and Domain Boundaries

Review the technical accuracy and completeness of AI concepts and systems, including:

- **AI approaches:** distinguish AI from machine learning and deep learning where the distinction matters. Review search, planning, knowledge representation, reasoning, and rule-based systems when discussed; do not assume every AI system is learned.
- **Generative and foundation models:** check claims about language, image, audio, video, and multimodal generation. For LLMs, assess claims about tokenization, context windows, prompting, model outputs, and inference. For diffusion systems, assess claims about conditioning, latent representations, denoising, sampling, and inference controls at the level described.
- **AI application architecture:** assess model selection and integration, input/output handling, system components, dependencies, and stated operational assumptions.
- **Agents and orchestration:** distinguish an agent from a base model, a single model call, a fixed workflow, and a conventional program where relevant. Check descriptions of tool calling, routing, delegation, control flow, state, memory, and stopping behavior against the article's implementation.
- **RAG and knowledge access:** distinguish retrieval from generation; check the stated roles of embedding, indexing, retrieval, context construction, and answer generation. Assess whether claims about freshness, grounding, citations, or reduced hallucination are appropriately qualified.
- **Evaluation:** check whether a stated metric or test supports the claimed property. Distinguish component tests, task success, human evaluation, offline benchmarks, and production outcomes. Account for nondeterminism, model/version changes, prompt sensitivity, and benchmark limitations when material.
- **Responsible deployment:** assess relevant claims about privacy, data handling, bias, reliability, human oversight, access control, and misuse or failure risks in the described system.

Use `ml-technical-review` for the underlying learning procedure, statistical assumptions, training data, optimization, mathematical derivation, or model-quality claims. A topic can require both skills: for example, review diffusion architecture and inference behavior here, and review its training objective, statistics, or tensor mathematics under the ML skill.

## Review Standards

1. Read the relevant AI claims in context, including diagrams, code, configuration, and the behavior the post says those artifacts implement.
2. Identify the system boundary and assumptions: model/provider and version when given, inputs, tools, data sources, orchestration, deployment context, and whether the description is conceptual or implementation-specific.
3. Check claims against established AI concepts and the supplied implementation. Treat provider/framework behavior as version-dependent unless the post identifies a version or authoritative evidence is available.
4. Verify that terminology is used precisely. Explain distinctions only when conflation affects the reader's understanding or the conclusion.
5. Evaluate whether evidence supports the strength of the claim. Separate a factual error from an overgeneralization, missing caveat, design trade-off, or claim that cannot be checked from the supplied information.
6. For code-level behavior, make only static observations unless the code is actually run in a suitable environment. Do not infer hidden framework defaults.
7. Prefer a narrow correction tied to the described use case over an unsupported universal rule.

## Evidence and Finding Format

For each material finding:

- Identify the section and a short quote, diagram element, or code location.
- State the claim or behavior at issue and why it is wrong, misleading, or under-specified.
- Explain the consequence for the reader or system understanding.
- Provide a correction, qualification, or specific verification need.
- Name assumptions and uncertainty. Use “cannot determine from the post” when required details are absent.

Prioritize material technical errors and misleading safety, reliability, or evaluation claims above optional depth. Return `PASS` when no material AI-specific issue is supported by the post. Do not create a finding solely to suggest additional breadth.

## Constraints

- Do not fabricate model or framework capabilities, API behavior, citations, benchmark results, or safety guarantees.
- Do not treat generated outputs as deterministic unless that property is established for the described setup.
- Do not present RAG, tool use, multi-agent design, or a larger model as an automatic guarantee of factuality, correctness, or safety.
- Do not conflate an AI system's observed behavior with a property guaranteed by its model or architecture.
- Do not judge a claim as incorrect solely because it omits detail irrelevant to its stated scope.
- Do not perform copyediting, audience review, or general code-integrity review; report only AI technical rigor issues.
- Do not edit the source or silently rewrite the post.

## Relationship to the ML Skill

Apply the AI skill to AI system, architecture, interaction, evaluation, and deployment claims. Apply `ml-technical-review` to learning, data, statistical, optimization, and mathematical claims. For overlap, analyze each claim under the domain that governs it and avoid duplicate findings. If the AI behavior depends on an ML assumption, state that dependency and refer to it in the finding.
