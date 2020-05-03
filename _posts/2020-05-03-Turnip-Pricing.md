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

Turnip is a fascinating distraction in _Animal Crossing: New Horizons_, and arguably what promotes the game's social aspect from a cute addition to an absolute necessity. In this post, 

## The Stalk Market Explained
Turnip, though appears to be a commodity at first glance, behaves very much like an American option -
* You pay a premium upfront every Sunday
* Every morning and afternoon the following Monday to Saturday, a new quote will be given in Nook's Cranny.
* The whole thing expires the next Sunday

But it's also different from an American option in at least one meaningful way. The only thing you can do to cash it out is to exercise it, as you won't be able to sell it to anyone else, which might have unintended ramification if we blindly borrow from the American option pricing machinery. In the absence of an optimal exercising strategy (comment if you know better!), I am going to make one assumption that makes the problem far more tractable: let's only exercise our "turnip option" at one specific time window (out of 12) when the Sharpe ratio return is the highest.

## Turnip's Price Dynamics
Thanks to the extraordinary reverse-engineering work done by Ash Wolf (see [here](https://gist.github.com/Treeki/85be14d297c80c8b3c0a76375743325b)), the price of a turnip can be numerically simulated.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/turnip_price.png" />
</div>


| Time | Expected Return | Volatility | Sharpe Ratio |
|---|---|---|---|
| Monday a.m. | -0.0895 | 0.2211 | -0.4049 |
| Monday p.m. | -0.1115 | 0.2379 | -0.4687 |
| Tuesday a.m. | -0.085 | 0.3118 | -0.2725 |
| Tuesday p.m. | 0.0462 | 0.6951 | 0.0664 |
| **Wednesday a.m.** | **0.0953** | **0.7169** | **0.1329** |
| Wednesday p.m. | 0.092 | 0.7133 | 0.129 |
| Thursday a.m. | 0.0754 | 0.7238 | 0.1042 |
| Thursday p.m. | 0.0829 | 0.7229 | 0.1147 |
| Friday a.m. | 0.0437 | 0.7328 | 0.0596 |
| Friday p.m. | -0.0361 | 0.7379 | -0.049 |
| Saturday a.m. | -0.2054 | 0.3844 | -0.5343 |
| Saturday p.m. | -0.2562 | 0.3297 | -0.7771 |

It's clear. If we have to fix our timing of selling, Wednesday a.m. seems to be the optimal choice both in terms of expected return and Sharpe ratio.

## Strategy: Sell on Wed a.m. and Go Away




## A Better Strategy: What if You have Friends?
To make things more interesting, the game also lets you exercise your "turnip option" on a friend's island. Let $P_1$, $P_2$, ..., $P_N$ be the turnip prices observed on $N$ different islands. Assuming they are IID and follow the cumulative distribution function of

$$
F_P(x) = G(x)
$$

the maximum value $Q$ where $Q = max(P_1, P_2, ..., P_N)$ will have the cumulative distribution function of:

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

