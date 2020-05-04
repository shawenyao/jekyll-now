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

And also, how having friends makes the stalk market a lot more profitable.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/001.jpg" />
</div>

_This is Part II of my Animal Crossing post series. For Part I, see [here](/Where-is-My-Island/)_.

Turnip is a fascinating addition in _Animal Crossing: New Horizons_, and arguably what promotes the game's social aspect from a cute distraction to an absolute necessity (if you want to play optimally). It is the de facto stock market on the deserted island, where you strive to buy low and sell high in order to pocket a decent profit. Plus, you can even visit your friends' island for some additional trading opportunity.

In this post, I examine the "stalk" market through the mean-variance optimization lens. 

## The Stalk Market Explained
Turnip, though appears to be a commodity, behaves very much like an American option -
* You pay a premium upfront every Sunday
* Every morning and afternoon of the following Monday to Saturday, a new quote will become avariable at Nook's Cranny.
* The whole thing expires the next Sunday

However, it's also different from an American option in at least one meaningful way. The only thing you can do to cash it out is to exercise it, as you won't be able to sell it to anyone else, which might have unintended ramification if we decide to borrow from the American option pricing machinery. In the absence of an optimal exercising strategy (comment if you know better!), I am going to make one assumption that makes the problem far more tractable: we can only exercise our "turnip option" at one specific time window (out of the total 12), and such decision will be soley based on [Sharpe ratio](https://en.wikipedia.org/wiki/Sharpe_ratio).

## Turnip's Price Dynamics
For a long time, it has been known to the Animal Crossing community that the turnip price isn't truly random. Instead, it follows one of the four following [patterns](https://animalcrossing.fandom.com/wiki/White_turnip):
* Random 
* Decreasing
* Large Spike
* Small Spike

Now thanks to the extraordinary reverse-engineering work done by Ash Wolf (see [here](https://gist.github.com/Treeki/85be14d297c80c8b3c0a76375743325b)), the turnip price dynamics has been uncovred in its entirety, to the point where it even becomes possible to simulate the prices numerically, enabling Monte-Carlo-style analysis:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/turnip_price.png" />
</div>


## Strategy: Sell on Wed a.m. and Go Away

Juding from my experiment of 100000 trials, if we have to fix our timing of selling turnips to one of the 12 time slots, Wednesday a.m. seems to be the best choice both in terms of expected return and Sharpe ratio. If we follow this strategy, a return of almost 10% can be expected over the 3-day time - significantly outperforming virtually every asset class in the real world, mind you. See appendix for details.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/turnip_return.png" />
</div>

## A Better Strategy: What if You have Friends?
To make things more interesting, the game also allows you to buy (on Sunday) and exercise your "turnip option" (in the following week) on a friend's island. . Let $P_1$, $P_2$, ..., $P_N$ be the turnip prices observed on $N$ different islands. Assuming they are IID and follow the cumulative distribution function of

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
| 2 | 0.4707 | 0.8983 | 0.524 |
| 3 | 0.7221 | 1.0167 | 0.7102 |
| 4 | 0.92 | 1.1097 | 0.829 |
| 5 | 1.0824 | 1.1853 | 0.9132 |
| 6 | 1.2234 | 1.2495 | 0.979 |
| ... | ... | ... | ... |

