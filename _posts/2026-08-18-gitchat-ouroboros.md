---
layout: post
title: "GitChat: Branching Conversations, For Real This Time"
categories: [claude-artifacts]
tags: [gitchat, ouroboros, claude, branching-conversation, git, ai-tools, spec-first-development]
description: >
  A follow-up to my mindmap-conversation Claude Artifact: GitChat is a self-hosted app where every
  conversation is a git repo, every message a commit, and every fork a branch — built with the
  Ouroboros spec-first workflow.
---

# GitChat: Branching Conversations, For Real This Time

Last year I posted a [Claude Artifact that turns conversations into a mindmap]({% post_url 2025-07-01-mindmap-conversation-claude %}) — breaking free from linear chat by branching into multiple threads. It was a prototype living inside an artifact sandbox, and I always wanted the real thing.

**[GitChat](https://github.com/Jaeha0526/gitchat)** is that follow-up: a self-hosted, open-source chat app where the branching isn't a UI metaphor — it's *actual git*.

- **Every conversation is a local git repo**
- **Every message is a commit**
- **Forking a conversation creates a git branch**
- **No database** — git *is* the database

An interactive tree in the sidebar maps every path you've explored: regenerate an answer, branch off a tangent at any message, abandon a dead-end and continue from where things were good. Each branch carries its full root-to-tip history as the AI's context. Built with Next.js and the Claude API.

## The Ouroboros experience

The part worth writing about is *how* it was built. I used [Ouroboros](https://github.com/Q00/ouroboros), a specification-first workflow that sits on top of your coding agent. Instead of prompting incrementally, Ouroboros interviews you until the ambiguity in what you want is driven down, then crystallizes everything into a seed spec — goal, constraints, acceptance criteria, even a domain ontology — that the agent builds against.

My seed for GitChat said things like *"each message stored as a git commit; branching creates a git branch"* and *"no external database — git is the database"*, with a dozen acceptance criteria covering the tree graph, hover previews, click-to-navigate, and zoom.

What impressed me: **with a clear idea of what I wanted, it produced a genuinely well-working repo.** Not a scaffold to fix up — a working app matching the spec. The lesson I took away is that the bottleneck has moved. The hard part is no longer writing the code; it's knowing precisely what you want. (That observation — that the *taste and intent* side is now the scarce resource — is exactly what led to [kkanbu]({% post_url 2026-08-18-kkanbu-research-taste %}).)

{% include share-buttons.html %}
