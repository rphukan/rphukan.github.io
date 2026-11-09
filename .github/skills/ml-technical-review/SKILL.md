---
name: ml-technical-review
description: 'Authoritative technical review guidance for Machine Learning blog posts about data, statistical learning, model objectives, optimization, deep learning, evaluation, generalization, and mathematical claims. Use when reviewing ML theory or practice.'
---

# Machine Learning Technical Review

Use this skill as the authoritative source for the scope, standards, constraints, and evidence practices when reviewing Machine Learning theory, methods, data, and model claims. Apply it alongside `ai-technical-review` when the post also makes claims about AI system architecture, generative applications, agents, or deployment behavior.

## When to Use This Skill

- Review posts about supervised, unsupervised, self-supervised, or reinforcement learning.
- Review data preparation, feature engineering, training, validation, optimization, or inference methods.
- Review statistical or mathematical claims, equations, loss functions, algorithms, model architectures, or tensor shapes.
- Review claims about model quality, generalization, uncertainty, calibration, or evaluation.

## Scope and Domain Boundaries

Review the technical validity of learning methods and claims, including:

- **Problem formulation:** identify the prediction or decision task, target, features, assumptions, and learning setup. Check that the selected method and objective fit the stated problem.
- **Data and preprocessing:** examine sampling, labels, splits, transformations, imputation, scaling, feature selection, augmentation, and class handling. Look for train/test leakage, temporal or group leakage, target leakage, and preprocessing fitted using held-out data.
- **Objectives and optimization:** check loss/objective definitions, regularization, optimizer updates, gradients, convergence claims, and how the stated algorithm relates to the objective. Distinguish minimizing a training objective from finding a global optimum or guaranteeing generalization.
- **Mathematics and representations:** verify algebra, notation, indices, shapes, dimensions, units, assumptions, and derivations. Ensure equations and prose describe the same computation.
- **Modeling:** check claims about linear/logistic models, neural networks, deep learning, generative learning, and other model classes in the context and conditions stated. Avoid treating a model family as universally best or making architectural guarantees unsupported by the setup.
- **Evaluation:** assess whether metrics, baselines, validation procedures, and uncertainty estimates support the conclusion. Check class imbalance, threshold choices, repeated tuning on test data, sample size, distribution shift, and whether reported metrics match the task.
- **Generalization and limitations:** distinguish training fit from held-out performance and deployment performance. Qualify claims affected by data distribution, sample size, model capacity, assumptions, randomness, or compute.

Use `ai-technical-review` for system-level AI behavior, prompting, generation, agent design, retrieval architecture, application evaluation, and deployment concerns. For a post about an AI model, review its learning objective and statistical claims here, and review its system or application behavior under the AI skill.

## Review Standards

1. Read the full relevant explanation, equations, figures, and code context before judging a claim.
2. Reconstruct the stated problem and assumptions. Do not silently fill gaps with an idealized formulation.
3. Check equations dimensionally and algebraically. Track indices, reduction conventions, units, and whether symbols have consistent meanings.
4. Trace the data lifecycle from collection and split through preprocessing, tuning, and evaluation. Identify where information can cross boundaries.
5. Check that optimization, loss, regularization, and evaluation correspond to the task. State when multiple conventions are valid.
6. Distinguish theoretical guarantees, empirical observations, heuristics, and recommendations. Verify that the wording does not overstate what the method ensures.
7. Make conclusions conditional on missing parameters or assumptions. A lack of implementation detail is not automatically proof of an error.
8. For framework code, separate mathematical issues from API questions. Do not assert version-specific behavior without version context or verification.

## Evidence and Finding Format

For each material finding:

- Identify the section and a short quote, equation, figure, or code location.
- State the technical claim and the assumptions under which it can be evaluated.
- Explain the contradiction, derivation, dimensional mismatch, leakage path, or unsupported inference.
- Provide a focused correction, qualification, or specific missing information needed to verify it.
- Distinguish a confirmed error from a nuance, limitation, or unverifiable claim.

Prioritize errors that change the method, result, or reader's understanding. Return `PASS` when no material ML-specific issue is supported by the post. Do not invent issues to make the review appear comprehensive.

## Constraints

- Do not fabricate data, experimental results, proofs, citations, or implementation behavior.
- Do not claim that a method converges, is unbiased, is optimal, or generalizes without the assumptions needed for that claim.
- Do not treat a metric as sufficient evidence unless it measures the property being claimed.
- Do not call a preprocessing step leakage without identifying what information crosses which evaluation boundary.
- Do not report stylistic preferences or code formatting issues as ML defects.
- Do not edit the source or silently rewrite the post.

## Relationship to the AI Skill

Apply this skill to learning procedures, data, statistical reasoning, objectives, optimization, model evaluation, and mathematics. Apply `ai-technical-review` to AI system and application behavior. For overlap, analyze the specific claim under the appropriate skill and avoid duplicate findings. If an AI-system conclusion depends on a learning or statistical assumption, identify that dependency.
