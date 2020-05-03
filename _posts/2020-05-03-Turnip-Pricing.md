---
layout: post
title: Turnip Pricing
tag:
  - maths
  - finance
  - animal crossing
comments: true
draft: true
---

And how having friends makes the stalk market a lot more profitable.

_This is Part II of my Animal Crossing post series. For Part I, see [here](/Where-is-My-Island/)_.

Turnips, though appears to be a commodity at first glance, behaves very much like an American option.


## Problem Formulation
Let $P_1$, $P_2$, ..., $P_N$ be the turnip prices observed on $N$ different islands. Assuming they are IID and follow the cumulative distribution function of

$$
F_P(x) = G(x)
$$

what are the distribution, expected value and standard deviation for $Q$ where $Q = max(P_1, P_2, ..., P_N)$ ?

## General Solution

$$
\begin{align}
F_Q(x) 
&= \mathbb{P}(Q \leq x) \\
&= \mathbb{P}(max(P_1, P_2, ..., P_N) \leq x) \\
&= \mathbb{P}(P_1 \leq x \ ∩ \ P_2 \leq x \ ∩ \ ... \ ∩ \ P_N \leq x) \\
&= \mathbb{P}(P_1 \leq x) \mathbb{P}(P_2 \leq x) \mathbb{P}(P_N \leq x) \\
&= G^{N}(x) \\
\end{align}
$$

## Final Thoughts
Note that for the purpose of this exercise, a risk-free rate of 0 is assumed. This really isn't as bad as it sounds for 2 reasons:
* starting from April 23rd, [the in-game interest rate has been slashed to near-zero](https://kotaku.com/nintendo-slashes-interest-rates-in-animal-crossing-new-1843019628)
* on the island, interest doesn't accrue intramonth anyway

