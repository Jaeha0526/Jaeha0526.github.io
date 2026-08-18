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

**[who-to-meet](https://github.com/Jaeha0526/who-to-meet)** answers a question everyone has at a conference or hackathon: *out of all these people, who should I actually talk to — and why?*

It ingests participant data (transcripts, bios, LinkedIn text) into a knowledge graph, then uses an LLM to compute semantic edges between people — shared goals, complementary skills, overlapping experiences — and serves transparent recommendations where every suggestion traces back to source data. No shallow "you both like AI" matching; you see the actual reasoning chain, explore an interactive force-directed graph, and chat with an agent about who to meet.

![The participant knowledge graph from Ralphthon SF — 15 people, semantic edges computed between every pair](/assets/img/blog/w2m-graph.png)

## The real experiment

The app is useful, but the *build process* was the point. This was my first serious test of [kkanbu]({% post_url 2026-08-18-kkanbu-research-taste %}), my taste oracle, paired with [Ouroboros](https://github.com/Q00/ouroboros) — the spec-first workflow that interviews you with Socratic questions until the ambiguity of what you want is driven down.

The twist: **I didn't answer the interview. kkanbu did, as my proxy.**

1. **Ouroboros** generated interview questions to crystallize requirements
2. **kkanbu** answered them from its typed knowledge graph of my preferences
3. **Claude Code** mediated between the two, executed builds, reviewed code, and committed
4. After each iteration: evaluate → consult kkanbu → interview → seed → run → repeat

Built at Ralphthon SF (March 2026): **~45 minutes of AI execution time, three iterations**, working app — with my taste in the loop but not my time.

## What it proved

The requirements interview is exactly the kind of subjective, preference-heavy conversation people assume needs the human present. It turns out an explicit, queryable taste artifact answers it well enough to ship software. That result is what pushed me to scale the same principle from "build me an app" to "run a research program" — see [An AI Scientist that Doesn't Drift]({% post_url 2026-08-18-ai-scientist-kkanbu %}).

{% include share-buttons.html %}
