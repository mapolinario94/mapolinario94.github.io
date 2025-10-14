---
layout: page
title: Adaptive Intelligence
description: Enabling Continual Learning on the Edge
img: assets/img/adaptive_intelligence.png
og_image: assets/img/adaptive_intelligence.png
importance: 2
category: research
related_publications: true
---

Deep neural networks today excel at learning complex representations from massive datasets — yet they remain inherently **static**. Once trained, they struggle to incorporate new knowledge without overwriting the old, a phenomenon known as *catastrophic forgetting*. Moreover, their reliance on global gradient backpropagation requires storing large activation maps and synchronizing updates across all layers — a process that is **energy-intensive** and **ill-suited for on-device intelligence**.

In contrast, natural intelligence learns **continuously** and **adaptively**. The brain integrates new experiences without erasing the past, leveraging distributed representations and sparse updates to maintain a stable sense of the world.

My research explores a simple yet profound question:

> *Can we build artificial systems that learn like the brain — efficiently, continuously, and autonomously on the edge?*

This question guides my work on **adaptive intelligence** — algorithms that allow deep networks to learn new tasks sequentially while preserving prior knowledge, all under the strict memory and energy constraints of embedded devices.



The first step toward this goal was to overcome **catastrophic forgetting** — the tendency of deep networks to lose prior knowledge when learning new tasks. In **CODE-CL (Conceptor-Based Gradient Projection for Deep Continual Learning)** {% cite Apolinario2025codecl %}, we introduced a biologically inspired framework where each task’s learned knowledge is encoded as a *conceptor matrix* — a compact representation of the activation subspace spanned by that task.

When learning a new task, CODE-CL projects incoming gradients onto the *pseudo-orthogonal* complement of previously learned subspaces, preventing destructive interference while still allowing information flow along shared directions. This mechanism effectively balances **stability and plasticity**: it preserves important gradient directions from past tasks while enabling **forward knowledge transfer** for new ones.
Through extensive experiments on benchmark datasets such as Split CIFAR-100, Split MiniImageNet, and 5-Datasets, CODE-CL demonstrated higher accuracy and reduced forgetting compared to state-of-the-art continual learning methods — all with minimal memory overhead and high computational efficiency.

Yet, while CODE-CL addressed *how to remember*, it also revealed the challenge of *where to learn efficiently*. Training deep networks, even for continual adaptation, still demands large activation storage for backpropagation — a severe limitation for edge devices with only a few hundred kilobytes of on-chip memory.

To address this, we developed **LANCE (Low-Rank Activation Compression for Efficient On-Device Continual Learning)** {% cite Apolinario2025lance %}, a framework that rethinks backpropagation itself. LANCE performs a **one-shot higher-order singular value decomposition (HOSVD)** to identify a reusable low-rank subspace for each layer’s activations.
Instead of recomputing decompositions every iteration, activations are projected into this fixed subspace throughout training — drastically reducing both memory and compute cost. This design reduces activation storage by up to **250×** and computational energy by **1.5×**, while maintaining accuracy within **2% of full backpropagation**.

Crucially, these fixed low-rank subspaces naturally extend to continual learning. Each new task is allocated to orthogonal components of the subspace, allowing models to **acquire new knowledge without overwriting the old**, and doing so entirely on-device. LANCE thus unifies compression and continual adaptation into a single mechanism, enabling edge devices to fine-tune and learn continually without relying on cloud resources or replay buffers.

Together, **CODE-CL** and **LANCE** define a roadmap toward **adaptive edge intelligence** — systems that learn efficiently, preserve knowledge over time, and adapt to changing environments. By coupling subspace-based memory preservation with low-rank activation compression, this research bridges algorithmic design and hardware co-optimization, paving the way for energy-efficient, lifelong learning in next-generation embedded and neuromorphic AI systems.

