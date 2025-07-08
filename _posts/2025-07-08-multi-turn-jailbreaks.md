---
layout: post
title: "Multi-Turn Jailbreaks Are Simpler Than They Seem"
categories: [research]
tags: [ai-safety, jailbreaks, llm, security]
description: >
  Empirical analysis revealing that multi-turn jailbreak attacks on LLMs are equivalent to resampling single-turn attacks, challenging assumptions about attack sophistication.
---

# Multi-Turn Jailbreaks Are Simpler Than They Seem

## Abstract

While defenses against single-turn jailbreak attacks on Large Language Models (LLMs) have improved significantly, multi-turn jailbreaks remain a persistent vulnerability, often achieving success rates exceeding 70% against models optimized for single-turn protection. This work presents an empirical analysis of automated multi-turn jailbreak attacks across state-of-the-art models including GPT-4, Claude, and Gemini variants, using the StrongREJECT benchmark.

## Key Findings

Our research challenges the perceived sophistication of multi-turn attacks:

### 1. Equivalence to Single-Turn Resampling
When accounting for the attacker's ability to learn from how models refuse harmful requests, multi-turn jailbreaking approaches are approximately equivalent to simply resampling single-turn attacks multiple times.

### 2. Correlated Attack Success
Attack success is correlated among similar models, making it easier to jailbreak newly released ones based on patterns observed in existing models.

### 3. Reasoning vs. Safety Trade-off
For reasoning models, we find surprisingly that higher reasoning effort often leads to higher attack success rates, suggesting a fundamental tension between reasoning capabilities and safety measures.

## Implications

Our results have important implications for:
- **AI Safety Evaluation**: Current multi-turn jailbreak evaluations may overestimate attack complexity
- **Defense Design**: Focusing on single-turn defenses may be more effective than previously thought
- **Model Development**: The trade-off between reasoning and safety needs careful consideration

## Methodology

We conducted systematic experiments using:
- **Models**: GPT-4, Claude, and Gemini variants
- **Benchmark**: StrongREJECT dataset
- **Approach**: Automated multi-turn attack generation and analysis

## Research Impact

This work provides crucial insights for the AI safety community, suggesting that current defensive strategies may be misdirected. By understanding that multi-turn attacks are fundamentally similar to repeated single-turn attempts, researchers can focus on more effective defense mechanisms.

[Download Full Paper](/assets/files/Multi_turn_Jailbreaks_Project-2.pdf){:.btn .btn-primary}