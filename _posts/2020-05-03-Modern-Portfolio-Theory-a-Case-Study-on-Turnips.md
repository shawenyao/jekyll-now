---
layout: post
title: Modern Portfolio Theory&#58 a Case Study on Turnips
tag:
  - maths
  - finance
  - animal crossing
comments: true
draft: true
---

And how having friends makes the stalk market a lot more profitable.

_This is Part II of my Animal Crossing post series. For Part I, see [here](/Where-is-My-Island/)_.

Turnip is a fascinating distraction in _Animal Crossing: New Horizons_, and arguably what promotes the game's social aspect from a cute addition to an absolute necessity. In this post, I examine the "stalk" market from a mean-variance optimization lens.

## The Stalk Market Explained
Turnip, though appears to be a commodity, behaves very much like an American option -
* You pay a premium upfront every Sunday
* Every morning and afternoon of the following Monday to Saturday, a new quote will become avariable at Nook's Cranny.
* The whole thing expires the next Sunday

But it's also different from an American option in at least one meaningful way. The only thing you can do to cash it out is to exercise it, as you won't be able to sell it to anyone else, which might have unintended ramification if we decide to borrow from the American option pricing machinery. In the absence of an optimal exercising strategy (comment if you know better!), I am going to make one assumption that makes the problem far more tractable: let's only exercise our "turnip option" at one specific time window (out of 12) with the highest Sharpe ratio.

## Turnip's Price Dynamics
It has always been known to the Animal Crossing community that the turnip prices follows one of the four following [patterns](https://animalcrossing.fandom.com/wiki/White_turnip):
* Random 
* Decreasing
* Large Spike
* Small Spike

Now thanks to the extraordinary reverse-engineering work done by Ash Wolf (see [here](https://gist.github.com/Treeki/85be14d297c80c8b3c0a76375743325b)), it is even possible to simulate the price paths numerically, enabling Monte-Carlo-style analysis:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/turnip_price.png" />
</div>


## Strategy: Sell on Wed a.m. and Go Away

Based on my experiment of 100000 trials, if we have to fix our timing of selling turnips, Wednesday a.m. seems to be the best choice in terms of both expected return (around 10%) and Sharpe ratio (0.13). See appendix for details.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/turnip_return.png" />
</div>



## A Better Strategy: What if You have Friends?
To make things more interesting, the game also allows you to exercise your "turnip option" on a friend's island. Let $P_1$, $P_2$, ..., $P_N$ be the turnip prices observed on $N$ different islands. Assuming they are IID and follow the cumulative distribution function of

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

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/turnip_return_multiple_islands.png" />
</div>

## Final Thoughts
Note that for the purpose of this exercise, a risk-free rate of 0 is assumed. This really isn't as bad as it sounds for two reasons:
* starting from April 23rd, the interest rate has been slashed to [near-zero](https://kotaku.com/nintendo-slashes-interest-rates-in-animal-crossing-new-1843019628)
* the in-game interest doesn't accrue intramonth anyway

## Appendix

Table 1: Optimal Selling Window

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

Table 2: Sellling on the Optimal Island

| Number of Islands | Expected Return | Volatility | Sharpe Ratio |
|---|---|---|---|
| 1 | 0.0953 | 0.7169 | 0.1329 |
| 2 | 0.4206 | 0.8689 | 0.484 |
| 3 | 0.6342 | 0.9667 | 0.6561 |
| 4 | 0.8027 | 1.0465 | 0.767 |
| 5 | 0.9418 | 1.1093 | 0.849 |
| 6 | 1.0623 | 1.1643 | 0.9124 |
