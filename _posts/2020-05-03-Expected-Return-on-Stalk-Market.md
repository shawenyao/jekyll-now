---
layout: post
title: Expected Return On Stalk Market
tag:
  - maths
  - animal crossing
comments: true
draft: true
---

How having friends makes the turnip business a lot more profitable.

## Problem Formulation

Let $P_1$, $P_2$, ..., $P_N$ be the turnip prices observed on $N$ different island. What are the distribution, expected value and variance for $Q$ where $ = max(P_1, P_2, ..., P_N)$ ?

## 
Assuming IID distribution of $P_1$, $P_2$, ..., $P_N$ and follows the cumulative distribution function of

$$
F_P(x) = G(x)
$$

We have:
$$
\begin{align}
F_Q(x) 
& = \mathbb{P}(Q < x)
& = \mathbb{P}(max(P_1, P_2, ..., P_N) < x)
& = \mathbb{P}(P_1 < x ∩ P_2 < x ∩ ... ∩ P_N < x)
& = \mathbb{P}(P_1 < x) \mathbb{P}(P_2 < x) \mathbb{P}(P_N < x)
& = {G(x)}^N
\end{align}
$$
