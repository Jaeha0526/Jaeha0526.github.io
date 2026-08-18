---
layout: post
title: "who-to-meet: An App Built by Interviewing My Taste Oracle"
hook: >
  An app built in 45 minutes where I never answered a single requirements question. The interview happened — my taste oracle sat in for me.
categories: [projects]
tags: [who-to-meet, ouroboros, kkanbu, hackathon, knowledge-graph, ai-tools]
image:
  path: /assets/img/blog/w2m-graph.png
description: >
  At Ralphthon SF 2026 I built an AI networking recommender in ~45 minutes of AI execution time —
  without answering a single requirements question myself. Ouroboros interviewed, kkanbu answered
  as my proxy, and Claude Code built.
---

# who-to-meet: An App Built by Interviewing My Taste Oracle

*Built at the SF Ralphthon hackathon, March 2026. [Code](https://github.com/Jaeha0526/who-to-meet)*

**[who-to-meet](https://github.com/Jaeha0526/who-to-meet)** answers a question everyone has at a conference or hackathon: *out of all these people, who should I actually talk to — and why?*

## What it does

It ingests participant data — conversation transcripts (Korean or English), bios, LinkedIn text — and uses a reasoning model (OpenAI o3) to extract structured profiles: interests, skills, traits, goals. Then it computes **semantic edges between every pair of participants**, analyzing each pair for deep connections, and serves the result three ways:

- **Graph + Chat** — an interactive force-directed knowledge graph; click any node for a full profile, click any *edge* to see why two people are connected, and ask the chat agent "who should I talk to about X?"
- **Knowledge Dashboard** — browse everyone as cards with detailed profiles and connection histories
- **Fun Matches** — generated pairings like *Startup Co-founders*, *Brain Trust*, *Most Unlikely But Perfect Pair*, and *Person Who Would Challenge Your Worldview*

![The participant knowledge graph from Ralphthon SF — 15 people, semantic edges computed between every pair](/assets/img/blog/w2m-graph.png)

The core design bet: **transparency over matching scores.** No shallow "you both like AI." Every recommendation exposes its reasoning chain, traced back to source data — o3 produces edges like *"both pivoted from creative fields to engineering and share a frustration with tools that hide their reasoning."* Under the hood it's deliberately simple: FastAPI + NetworkX + SQLite on the backend (no graph database needed for 20 people), Next.js + react-force-graph-2d on the front.

## The real experiment

The app is useful, but the *build process* was the point. This was my first serious test of [kkanbu]({% post_url 2026-08-18-kkanbu-research-taste %}), my taste oracle, paired with [Ouroboros](https://github.com/Q00/ouroboros) — the spec-first workflow that interviews you with Socratic questions until the ambiguity of what you want is driven down.

The twist: **I didn't answer the interview. kkanbu did, as my proxy.**

1. **Ouroboros** generated interview questions to crystallize requirements
2. **kkanbu** answered them from its typed knowledge graph of my preferences
3. **Claude Code** mediated between the two, executed builds, reviewed code, and committed
4. After each iteration: evaluate → consult kkanbu → interview → seed → run → repeat

Three iterations, ~45 minutes of total AI execution time:

- **Iteration 1** (~14 min): full-stack app build — FastAPI + Next.js + graph + chat, 14/14 acceptance criteria
- **Iteration 2** (~9 min): semantic edges via o3, chat persistence, fun matches, UX polish, 12/12
- **Iteration 3** (~8 min): 17 bug fixes, pytest tests, chat→graph sync, 11/11

## What it proved

The requirements interview is exactly the kind of subjective, preference-heavy conversation people assume needs the human present. It turns out an explicit, queryable taste artifact answers it well enough to ship working software. That result is what pushed me to scale the same principle from "build me an app" to "run a research program" — see [An AI Scientist that Doesn't Drift]({% post_url 2026-08-18-ai-scientist-kkanbu %}).

{% include share-buttons.html %}
