---
layout: post
title: "Exploring the Holographic Entropy Cone via Reinforcement Learning"
categories: [projects]
tags: [reinforcement-learning, holography, quantum-gravity, entropy-cone, physics]
image:
  path: /assets/img/blog/entropy-fig3.png
description: >
  Published in JHEP (2026). We develop a reinforcement learning algorithm that searches for graph
  realizations of entropy vectors, resolving the status of "mystery" extreme rays of the N=6
  holographic entropy cone and revealing that unknown holographic entropy inequalities must exist.
---

# Exploring the Holographic Entropy Cone via Reinforcement Learning

*With Temple He and Hirosi Ooguri. Published in [JHEP 06 (2026) 267](https://doi.org/10.1007/JHEP06(2026)267) ([arXiv:2601.19979](https://arxiv.org/abs/2601.19979)).*

## Overview

The holographic entropy cone (HEC) characterizes which entanglement entropy patterns are achievable in holographic quantum systems. Determining whether a given entropy vector lies inside the cone is a hard combinatorial problem: a vector is holographic if and only if it admits a **graph realization** whose min-cut entropies match the vector.

We developed a reinforcement learning algorithm that searches this space of graph realizations directly. Given a target entropy vector, the agent modifies a weighted graph to match the target's min-cut structure, with reward given by the cosine similarity between the achieved and target entropy vectors.

![The S3-symmetric slice of the N=3 entropy space with the RL reward landscape](/assets/img/blog/entropy-fig1.png)

## The algorithm as a probe

Two regimes make the method useful:

- **Classification** — if the agent reaches reward 1, the target vector admits a graph realization and lies inside the HEC.
- **Navigation** — if the target is *outside* the cone, the agent converges to the nearest realizable vector, and the reward gradient points toward the cone's boundary — probing the location of unknown facets.

## Results

- **N=3 validation**: the algorithm rediscovers monogamy of mutual information (MMI) starting from a target vector outside the cone, and its reward landscape matches analytical predictions with correlation 0.996.

![3D view of the reward landscape on the N=3 symmetric slice: analytical surface vs RL points](/assets/img/blog/entropy-fig3.png)

- **N=6 mystery rays**: we analyzed the six extreme rays of the subadditivity cone (from [arXiv:2412.15364](https://arxiv.org/abs/2412.15364)) that satisfy all known holographic entropy inequalities yet lacked graph realizations. Our algorithm **found realizations for three of them**, proving they are genuine extreme rays of the HEC.
- **Unknown inequalities exist**: for the remaining three rays we provide evidence that no realization exists — implying there are holographic entropy inequalities for N=6 that have not yet been discovered.

![Graph realizations of extreme rays 146, 180, and 181](/assets/img/blog/entropy-fig7.png)

## Companion tooling

Alongside the RL approach, I built [lp_ray_finder](https://github.com/Jaeha0526/lp_ray_finder), an LP-based active-set algorithm for finding extreme rays of convex cones at scales where standard vertex enumeration becomes infeasible (the N=6 system), with CPU-parallel and GPU-accelerated phases.

**Code**: [EntropyCone_RL](https://github.com/Jaeha0526/EntropyCone_RL)

This project is part of a broader theme I care deeply about: using modern ML not as a curve-fitter but as a **search engine over mathematical structures** — here, literally mapping the boundary of what quantum gravity allows.

{% include share-buttons.html %}
