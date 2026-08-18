---
layout: post
title: "Branching Conversations: From Claude Artifact to GitChat"
categories: [projects]
tags: [gitchat, ouroboros, claude, branching-conversation, mindmap, git, ai-tools, spec-first-development]
image:
  path: /assets/img/blog/gitchat-tree.png
description: >
  Breaking free from linear chat, in two acts: a mindmap-style branching conversation prototype
  built as a Claude Artifact, and GitChat — the real self-hosted app where every conversation is a
  git repo, every message a commit, and every fork a branch. Built with the Ouroboros spec-first workflow.
---

# Branching Conversations: From Claude Artifact to GitChat

Traditional conversations with AI follow a linear, back-and-forth pattern. But what if we could **branch out** and explore multiple discussion threads simultaneously?

## Act 1: The Claude Artifact prototype (2025)

My first take on this was a Claude Artifact that turns a conversation into a dynamic **mindmap**: instead of one flat message history, you branch at any point and explore multiple threads side by side.

[![Mindmap Conversation Interface](/assets/img/blog/mindmap-like-conversation.png)](https://claude.ai/public/artifacts/0b8d19e7-53f0-47a5-a41f-302f674af269)

**[🚀 Try the Live Artifact](https://claude.ai/public/artifacts/0b8d19e7-53f0-47a5-a41f-302f674af269)**

It worked, and it changed how I think about talking to AI — but it lived inside an artifact sandbox. I always wanted the real thing.

## Act 2: GitChat — branching for real (2026)

**[GitChat](https://github.com/Jaeha0526/gitchat)** is the follow-up: a self-hosted, open-source chat app where the branching isn't a UI metaphor — it's *actual git*.

- **Every conversation is a local git repo**
- **Every message is a commit**
- **Forking a conversation creates a git branch**
- **No database** — git *is* the database

An interactive tree in the sidebar maps every path you've explored: regenerate an answer, branch off a tangent at any message, abandon a dead-end and continue from where things were good. Each branch carries its full root-to-tip history as the AI's context. Built with Next.js and the Claude API.

Here it is running locally. The whole point is the **tree**: one conversation ("Why is the sky blue?") grew into 16 nodes across 5 branches — a deep physics derivation on `main`, a sunset tangent, an explain-like-I'm-five path, and two character branches. Every node is a git commit; clicking any node jumps you to that branch at that point:

![GitChat conversation tree: 16 nodes across 5 branches](/assets/img/blog/gitchat-tree.png)

Branching also makes **comparison** natural. GitChat supports AI characters (custom system prompts), so I forked the same question — *"Is the blueness of the sky a property of the sky itself, or something we create by looking at it?"* — into two branches, one asking a **Physicist** character, one asking a **Philosopher**. Same fork point, same context, two worldviews side by side:

![Same question, two characters: physicist vs philosopher branches](/assets/img/blog/gitchat-characters.png)

In a linear chat, the second answer would have overwritten the first; here both live permanently on their own branches, and I can keep developing either thread.

## The Ouroboros experience

The part worth writing about is *how* GitChat was built. I used [Ouroboros](https://github.com/Q00/ouroboros), a specification-first workflow that sits on top of your coding agent. Instead of prompting incrementally, Ouroboros interviews you until the ambiguity in what you want is driven down, then crystallizes everything into a seed spec — goal, constraints, acceptance criteria, even a domain ontology — that the agent builds against.

My seed for GitChat said things like *"each message stored as a git commit; branching creates a git branch"* and *"no external database — git is the database"*, with a dozen acceptance criteria covering the tree graph, hover previews, click-to-navigate, and zoom.

What impressed me: **with a clear idea of what I wanted, it produced a genuinely well-working repo.** Not a scaffold to fix up — a working app matching the spec. The lesson I took away is that the bottleneck has moved. The hard part is no longer writing the code; it's knowing precisely what you want. (That observation — that the *taste and intent* side is now the scarce resource — is exactly what led to [kkanbu]({% post_url 2026-08-18-kkanbu-research-taste %}).)

{% include share-buttons.html %}
