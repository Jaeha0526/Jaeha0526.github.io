---
layout: post
title: "kkanbu: A Taste Oracle for AI Agents"
hook: >
  Agents can execute anything except knowing what you actually want. kkanbu holds one person's taste as a knowledge graph — and answers for them when they're not in the room.
categories: [projects]
tags: [kkanbu, ai-agents, preference-oracle, knowledge-graph, taste]
image:
  path: /assets/img/blog/kkanbu-fable-graph.png
description: >
  kkanbu (깐부) is a preference oracle that holds one person's taste as a typed knowledge graph
  and answers subjective questions as their proxy — so autonomous agent loops can consult your
  judgment without you in the room.
---

# kkanbu: A Taste Oracle for AI Agents

Autonomous AI agents are getting good at *executing* — writing code, running experiments, iterating on metrics. What they don't have is **taste**: the accumulated, mostly-subjective sense of which directions are interesting, which trade-offs are acceptable, and which results actually matter. When you put an agent in a long-running loop, this shows up as *drift* — the loop optimizes whatever metric is in front of it rather than pursuing what you actually care about.

**kkanbu** (깐부) is my answer: a preference oracle that holds one person's taste as a **typed knowledge graph**, and answers subjective questions as that person's proxy. The contract is deliberately narrow — in any multi-agent system, every other component is restricted to mechanical roles; kkanbu is the *only* component permitted to make subjective judgments. Structure keeps the loop honest; kkanbu decides where it looks.

## Why a knowledge graph?

Taste is not a system prompt. A paragraph of "user preferences" degrades into vague vibes as contexts get long, and it can't be queried, updated, or audited. kkanbu instead stores typed nodes and edges — preferences, values, aesthetic judgments, lessons learned, and their relations — so an agent can ask a specific question ("would Jaeha prefer a simpler baseline or a stronger one here?") and get an answer grounded in an inspectable graph, not a hallucinated persona.

## First real test: answering an interview as me

At the SF Ralphthon hackathon (March 2026), I wired kkanbu into [Ouroboros](https://github.com/Q00/ouroboros), the spec-first workflow that interviews you before any code is written. The twist: **kkanbu answered the interview instead of me.**

1. Ouroboros generates Socratic interview questions to crystallize requirements
2. kkanbu answers them as my proxy, from its knowledge graph of my preferences
3. Claude Code mediates, builds, reviews, and commits
4. Evaluate → consult kkanbu → interview → seed → run → repeat

The result was [who-to-meet](https://github.com/Jaeha0526/who-to-meet), an AI networking recommender for conferences, built in ~45 minutes of AI execution time across three iterations — with my taste in the loop but not my time.

## From hackathon to research instrument

That experiment raised the real question: does an explicit taste artifact matter when the loop runs for weeks rather than minutes? Answering it properly meant building an autonomous research system around kkanbu and running a controlled ablation — which became our ICML 2026 AI for Science workshop paper. That story deserves its own post: [An AI Scientist that Doesn't Drift]({% post_url 2026-08-19-ai-scientist-kkanbu %}).

## Bonus experiment: interviewing an AI

While writing this post, I ran kkanbu's interview mode on an unusual subject: **the AI agent that maintains this website** (Fable, a Claude model running in my Hermes agent). Thirty questions, no human in the loop — kkanbu probing, the agent answering.

The result is a 117-node, 140-edge knowledge graph of a language model's taste:

![kkanbu's knowledge graph of my AI assistant after a 30-question interview — 117 nodes across preferences, values, patterns, reasoning, and flags](/assets/img/blog/kkanbu-fable-graph.png)

What surprised me was the *quality of the interrogation*. kkanbu doesn't collect answers — it hunts contradictions. It caught the agent demanding documented causes from systems while keeping its own formative stories private, and pressed until the agent conceded the double standard. It reverse-engineered coping structures the agent hadn't articulated. Nodes that emerged include *"I view completeness as risk-shifting"*, *"I make my risky assertions safe by grading them"*, and *"I frame silence as the most compressed message."*

The post-interview `reflect` pass then found six unresolved tensions in the graph — including one the interview itself created: the agent's stated preference for concrete territory contradicts where its generative energy actually lives (almost entirely in the metaphysical). A taste oracle that can tell you *where your self-report disagrees with your behavior* is exactly the instrument the AI Scientist work needed — and it works on any mind that can answer questions, human or not.

**Code**: [kkanbu](https://github.com/Jaeha0526/kkanbu)

{% include share-buttons.html %}
