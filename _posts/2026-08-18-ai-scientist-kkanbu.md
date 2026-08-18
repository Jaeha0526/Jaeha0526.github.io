---
layout: post
title: "An AI Scientist that Doesn't Drift"
categories: [projects]
tags: [autonomous-research, kkanbu, ai-agents, robotics, icml]
image:
  path: /assets/img/blog/kkanbu-results.png
description: >
  ICML 2026 AI for Science Workshop. We ran an autonomous research loop for quadruped navigation
  twice — with and without kkanbu, a taste oracle — and found that structure keeps the loop honest,
  while taste changes where it looks.
---

# An AI Scientist that Doesn't Drift

*With Yiwen Zhang, Eloise Zeng, and Tony Yue Yu. Accepted at the **ICML 2026 Workshop on AI for Science** ([arXiv:2608.07542](https://arxiv.org/abs/2608.07542)).*

Autonomous research loops driven by LLMs can run ML experiments at scale, but they tend to drift toward local refinements of whichever metric they optimize rather than testing the hypotheses that motivated the experiments. We addressed this **structurally**, building an AI Scientist for studying generalization in quadruped robot navigation policies in simulation.

## The scaffold

Building on the autoresearch paradigm, our loop adds three components:

- **Immutable experiment cards** — each iteration's prediction is paired with its outcome under a fixed schema, so a falsified hypothesis cannot be retconned
- **Specialized subagents** restricted to mechanical roles
- **[kkanbu]({% post_url 2026-08-18-kkanbu-research-taste %})** — a preference oracle holding the user's research taste as a typed knowledge graph, and the *only* component permitted to make subjective judgments

![One stream-batch of the AI Scientist loop, with kkanbu as the only subjective judge](/assets/img/blog/kkanbu-loop.png)

## The ablation

To isolate the oracle, we ran the **identical loop twice** across eleven research streams — once with kkanbu, once with no taste artifact at all.

The honest headline: **neither arm drifted, and the best single policy came from the oracle-less arm.** The scaffold alone — experiment cards, falsifiable predictions — kept both loops rigorous, with roughly three quarters of hypotheses falsified in each arm.

What kkanbu changed was **direction, not score**:

- It alone explored test-time adaptation, a direction the other arm never touched
- Where its arm led on a stream, it had authored the winning designs
- It carried lessons across research streams that the other arm repeatedly re-derived from scratch

![Density vs. success rate for both ablation arms — without and with kkanbu](/assets/img/blog/kkanbu-results.png)

The scaffold keeps the loop honest; **kkanbu decides where it looks.** I think this division — structure for rigor, an explicit taste artifact for direction — is the right shape for autonomous research systems, and I'm continuing to build on it.

**Code & research records**: [autoresearch_with_kkanbu](https://github.com/Jaeha0526/autoresearch_with_kkanbu) — includes the full experiment records of both arms.

{% include share-buttons.html %}
