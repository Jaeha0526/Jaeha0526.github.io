---
layout: post
title: "kkanbu: Giving AI Agents Your Research Taste"
categories: [research]
tags: [ai-agents, autonomous-research, preference-oracle, knowledge-graph, kkanbu, icml]
description: >
  From a hackathon experiment to an ICML 2026 workshop paper: kkanbu is a preference oracle that
  holds a researcher's taste as a typed knowledge graph, letting autonomous AI loops make
  subjective judgments the way you would — without drifting.
---

# kkanbu: Giving AI Agents Your Research Taste

Autonomous AI agents are getting good at *executing* — writing code, running experiments, iterating on metrics. What they don't have is **taste**: the accumulated, mostly-subjective sense of which directions are interesting, which trade-offs are acceptable, and which results actually matter. When you put an LLM in a long-running loop, this shows up as *drift* — the loop optimizes whatever metric is in front of it rather than pursuing the questions that motivated the work.

**kkanbu** (깐부) is my attempt at solving this: a preference oracle that holds one researcher's taste as a **typed knowledge graph**, and answers subjective questions as that researcher's proxy. Other agents in a system are restricted to mechanical roles; kkanbu is the only component permitted to make subjective judgments.

## First proof of concept: a hackathon interview

At the SF Ralphthon hackathon (March 2026), I tested the idea in a compressed setting. I paired kkanbu with [Ouroboros](https://github.com/Q00/ouroboros), a specification-first development workflow that begins by *interviewing* you — Socratic questions that drive down the ambiguity of what you want before any code gets written.

The twist: **kkanbu answered the interview instead of me.** The loop was:

1. Ouroboros generates interview questions to crystallize requirements
2. kkanbu answers them as my proxy, from its knowledge graph of my preferences
3. Claude Code mediates, builds, reviews, and commits
4. Evaluate → consult kkanbu → interview → seed → run → repeat

The result was [who-to-meet](https://github.com/Jaeha0526/who-to-meet), an AI-powered networking recommender for conferences, built in roughly 45 minutes of AI execution time across three iterations. A small thing, but it demonstrated the core mechanic: an agent loop can consult *your* taste without you in the room.

## Scaling up: an AI scientist that doesn't drift

That experiment led directly to the real question: does taste matter in *research*, where the loop runs for weeks rather than minutes?

With Yiwen Zhang, Eloise Zeng, and Tony Yue Yu, we built an AI Scientist for studying generalization in quadruped robot navigation policies (simulation), and ran the identical autonomous research loop **twice** across eleven research streams — once with kkanbu, once without any taste artifact. The work is accepted at the **ICML 2026 Workshop on AI for Science** ([arXiv:2608.07542](https://arxiv.org/abs/2608.07542)).

Beyond kkanbu, the loop adds structural honesty mechanisms:

- **Immutable experiment cards** — each iteration's prediction is paired with its outcome under a fixed schema, so a falsified hypothesis cannot be retconned
- **Specialized subagents** restricted to mechanical roles
- **kkanbu as the sole subjective judge**

## What we found

The honest headline: **neither arm drifted, and the best single policy came from the oracle-less arm.** The scaffold alone — experiment cards, falsifiable predictions — kept both loops rigorous, with roughly three quarters of hypotheses falsified in each arm.

What kkanbu changed was **direction, not score**:

- It alone explored test-time adaptation, a direction the other arm never touched
- Where its arm led on a stream, it had authored the winning designs
- It carried lessons across research streams that the oracle-less arm repeatedly re-derived from scratch

The scaffold keeps the loop honest; **kkanbu decides where it looks.** I think this division — structure for rigor, an explicit taste artifact for direction — is the right shape for autonomous research systems, and I'm continuing to build on it.

**Code & research records**: [autoresearch_with_kkanbu](https://github.com/Jaeha0526/autoresearch_with_kkanbu) — includes the full experiment records of both arms.

{% include share-buttons.html %}
