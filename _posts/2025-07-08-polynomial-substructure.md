---
layout: post
title: "Discovering Hidden Algebraic Structures via Transformers with Rank-Aware Beam GRPO"
categories: [research]
tags: [transformers, symbolic-reasoning, reinforcement-learning, mathematics]
description: >
  NeurIPS submission presenting a novel approach to multivariate polynomial decomposition using transformers and rank-aware reinforcement learning, achieving 75% reduction in inference compute.
---

# Discovering Hidden Algebraic Structures via Transformers with Rank-Aware Beam GRPO

## Abstract

We study the capabilities of small-scale transformer models in symbolic reasoning, focusing on the NP-hard algebraic task of multivariate polynomial decomposition, with widespread applications in science and engineering. Our approach includes a fine-grained synthetic data generation pipeline, supervised pretraining, beam search, evaluations for scaling behavior and generalizability, and a novel rank-aware reinforcement learning method called Beam Grouped Relative Policy Optimization (BGRPO), which improves accuracy while reducing inference compute by up to 75%.

## Key Contributions

### 1. Novel BGRPO Algorithm
We introduce **Beam Grouped Relative Policy Optimization (BGRPO)**, a rank-aware reinforcement learning method that:
- Improves decomposition accuracy
- Reduces inference compute by up to 75%
- Handles the sparse solution space of polynomial decomposition

### 2. Synthetic Data Pipeline
Our fine-grained synthetic data generation pipeline enables:
- Systematic training on polynomial decomposition tasks
- Controlled complexity scaling
- Comprehensive evaluation across difficulty levels

### 3. Competitive Performance
Our transformer-based model demonstrates:
- **Competitive performance** with traditional symbolic systems
- **Outperforms Mathematica** in various polynomial simplification cases
- Strong generalization across different polynomial structures

## Technical Approach

### Problem Definition
Functional decomposition poses significant challenges because:
- Sub-functions can be completely hidden in the final compact form
- Requires extreme precision with no margin of error
- Admits only a sparse set of correct solutions

### Methodology
1. **Supervised Pretraining**: Train transformers on synthetic polynomial data
2. **Beam Search**: Explore multiple decomposition candidates
3. **BGRPO**: Rank-aware reinforcement learning for optimization
4. **Evaluation**: Scaling behavior and generalizability analysis

## Research Impact

This work demonstrates that transformers can:
- **Discover hidden patterns** in mathematical structures
- **Compete with traditional symbolic systems** in specialized domains
- **Benefit from novel RL approaches** tailored to symbolic reasoning

### Applications
- Scientific computing and engineering
- Computer algebra systems
- Automated theorem proving
- Mathematical discovery

## Collaboration

**Authors**: Jaeha Lee, Gio Huh, Ning Su, Tony Yue Tu

This research represents a significant step forward in applying deep learning to symbolic mathematics, showing that transformers can excel in domains requiring precise symbolic manipulation.

[Download Full Paper](/assets/files/Polynomial_Substructure_NeurIps_Submission-11.pdf){:.btn .btn-primary}