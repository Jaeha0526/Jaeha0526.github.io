---
layout: post
title: "An Agentic System for Performing Representation Engineering for Character Control"
hook: >
  Personality lives somewhere inside a model's activations. We built an agentic system that finds those directions and steers character along them.
categories: [projects]
tags: [representation-engineering, llm, character-control, agentic-systems]
image:
  path: /assets/img/blog/repe-umap.png
description: >
  CS 159 final project: an automated multi-agent system that extracts emotion concept vectors from
  Llama-3-8B, steers its character along them, and wraps the result in guardrails — tested across
  42 emotions.
---

# An Agentic System for Performing Representation Engineering for Character Control

*With Deepro Pasha and Ananya Gangavarapu (Caltech CS 159). [Full report (PDF)](/assets/files/CS_159_Final_Project-3.pdf) · [Code](https://github.com/anigasan/CS1592025)*

Character in an LLM — its tendencies, patterns, and values — isn't just a prompt away. It lives in the model's internal representations, and **representation engineering (RepE)** can steer it there directly: extract a concept direction from contrastive data, then push activations along that direction at generation time. No retraining, no fine-tuning, precise control.

The catch is that doing RepE well is tedious: generating contrastive datasets, training readers per emotion per layer, evaluating whether steering actually worked. Our project turned that entire pipeline into an **agentic system** that runs it automatically.

## The system

Built on CrewAI, the system orchestrates specialized agents across the full RepE lifecycle against Meta-Llama-3-8B-Instruct:

- **Training agents** — an *Emotion Keyword Specialist* generates contrastive training data for a target emotion; a *RepReader Trainer* extracts direction vectors from it via PCA across all 31 layers
- **Evaluation agents** — a *Prompt Design Specialist* builds test scenarios where the emotion fits the context *and* where it conflicts; *Category* and *Overall* evaluators score baseline vs controlled outputs on emotion expression and appropriateness
- **Vector management agents** — a *Concept Vector Analyst* and *Vector Librarian* maintain a growing library of high-quality vectors, selecting and linearly combining them with fresh extractions
- **NeMo Guardrails** as a final safety layer, so steering toward an emotion can't push outputs into toxicity

## Findings

**Emotion representations are stable — and live in the middle layers.** Extracting the same emotion 15 independent times, cosine consistency concentrates around layers −12 to −15. Early layers haven't formed high-level semantics yet; late layers are busy producing output. The middle is where character lives.

**The emotion space has structure.** We extracted vectors for 42 distinct emotions (110 vectors total) and projected them with UMAP:

![UMAP projection of 110 concept vectors for 42 emotions extracted from Llama-3-8B-Instruct](/assets/img/blog/repe-umap.png)

Same-emotion vectors cluster tightly, and psychologically meaningful neighborhoods emerge — anger next to violence, love with heartwarming, nostalgia with loneliness and melancholy, confidence with pride. Intriguingly, the space splits into two macro-clusters whose organizing principle doesn't correspond to valence or arousal — some other axis of the model's emotional geometry we couldn't name.

**The vector library pays off.** In an ablation across 10 emotions (from anger to schadenfreude to wanderlust), combining fresh extractions with high-quality library vectors consistently beat fresh extraction alone:

![Effectiveness comparison: steering with vs without automated vector selection](/assets/img/blog/repe-effect.png)

## Why it matters

The automation is the point: testing 42 emotions with consistent methodology would be prohibitively slow by hand. An agentic wrapper turns RepE from a research technique into a systematic instrument — and the evaluation-feedback loop opens the door to self-improving steering systems that re-extract when consistency degrades. Character control with guardrails layered on top addresses both sides: precise steering *and* safe outputs.

{% include share-buttons.html %}
