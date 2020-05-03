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

## The Stalk Market Explained
Turnip, though appears to be a commodity at first glance, behaves very much like an American option -
* You pay a premium upfront every Sunday
* You wait for the optimal timing to sell as the turnip price fluctuates in the following week
* The whole thing expires in 7 days

But it's also different from an American option in at least one meaningful way. The only thing you can do to cash it out is to exercise it, as you won't be able to sell it to anyone else, which might have unintended ramification if we blindly borrow from the American option pricing machinery. In the absence of an optimal strategy (comment if you know better!), I am going to make one assumption that makes the problem far more tractable: let's only exercise our "turnip option" on Saturday night, i.e., at the last price available before it spoils.

## Turnip's Profit Distribution
Thanks to the extraordinary reverse-engineering work done by Ash Wolf (see [here](https://gist.github.com/Treeki/85be14d297c80c8b3c0a76375743325b)), the profit of our Saturday-night-only strategy can be numerically simulated.




## What if You have Friends?
To make things more interesting, the game also lets you exercise your "turnip option" on a friend's island. Let $P_1$, $P_2$, ..., $P_N$ be the turnip prices observed on $N$ different islands. Assuming they are IID and follow the cumulative distribution function of

$$
F_P(x) = G(x)
$$

the maximum value $Q$ where $Q = max(P_1, P_2, ..., P_N)$ will have the cumulative dsitribution function of:

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
Note that for the purpose of this exercise, a risk-free rate of 0 is assumed. This really isn't as bad as it sounds for two reasons:
* starting from April 23rd, the interest rate has been slashed to [near-zero](https://kotaku.com/nintendo-slashes-interest-rates-in-animal-crossing-new-1843019628)
* the in-game interest doesn't accrue intramonth anyway

