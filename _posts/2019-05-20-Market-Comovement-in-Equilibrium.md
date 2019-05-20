---
layout: post
title: Market Comovement in Equilibrium
tag:
  - finance
comments: true
draft: false
---

A glimpse of the promised land.

## Introduction

Arguably, one of the most intriguing phenomena of the market is its _dynamism_. Unlike physics where the law of nature is to a large extent independent of human awareness, market responds, adapts and evolves based on what we know about it. For starters, Fama and French's discovery of value and size effect led to a whole new school known as factor investing; likewise, we have never looked at options the same way since Black, Scholes and Merton uncovered the world of geometric Brownian motion; more commonly, arbitrageurs sniff around on a daily basis, exploiting mispricing until it goes way. In all of these instances, it is the knowledge we possess that leads to the action we take, leaving a permanent mark on how market behaves.

One of such curious cases is the modern portfolio theory. Harry Markowitz foresees a world where everybody holds the optimal risky asset. As the separation property states, investors move along the capital allocation line based on their individual risk preferences, holding a combination of the risk-free asset and the tangency portfolio. In equilibrium, the total supply equals the total demand, so the tangency portfolio has to be the value-weighted portfolio of all risky assets - or simply put, the market portfolio.

However, the story does not end there. Since the only way in which investors are willing to alter their exposure to risky assets is to adjust their positions in the market portfolio, every order placed on it exerts identical buying (or selling) pressure on all of its constituents. Upon successful fulfillment of such orders, each constituent's price goes up (or down) by the same amount percentage-wise and the market portfolio remains the value-weighted collection of all risky assets. It is along these lines that I show in this post the evidence that the market comovement is stronger than ever, and where it can lead us in equilibrium.

## Index Trading and Return Covariation

The S&P 500 index, widely considered to be a proxy of the market portfolio, provides a unique look at how differently an asset would behave upon joining the index trading universe in terms of covariation. For each of the constituents, we go back to the very date it was included in the index ($t = 0$) and examine its monthly correlation with the index in the preceding year ($-12 \leq t \leq 0$) as well as the subsequent year ($1 \leq t \leq 12$).

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study1_monthly_rho.svg" />
</div>

The difference is small yet significant. The paired two-sample t-test suggests the sheer volume of index trading is strong enough to make a dent in the way the index constituents covary with the index itself. On average, once becoming a constituent, the correlation between the asset and the index rises from 0.458 (as in the year before) to 0.505 (as in the year after).

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study3_pre_post_distribution.svg" />
</div>

Granted, the daily trading volume of the S&P 500 constituents that's attributable to index trading is far from dominant, and firm-specific news still play a major role in price discovery. However, whether we like it or not, there is also no denial that passive portfolio management is on the [rise](https://www.cnbc.com/2019/03/19/passive-investing-now-controls-nearly-half-the-us-stock-market.html), brining us ever so slightly closer to Harry Markowitz's promised land.


## A Comoving Market

The modern portfolio theory states that under the homogenous expectations assumption, every investor has the same view when it comes to estimating the expected return, volatility and correlation of all risky assets. Every investor then goes ahead and solves for the same mean-variance optimization problem and arrives at the same answer - the efficient frontier.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier1.svg" />
</div>

The limiting case of the S&P 500 index trading example will lead us to something fairly similar to Harry Markowitz's conceptual world of equilibrium, where
* every investor only holds the market portfolio as far as risky assets are concerned
* every transaction is done via trading the market portfolio

As mentioned earlier, the fact that market portfolio becomes the only trading vehicle will consequently make every individual risky assets that constitutes the market go up and down in price as one, implying the same return, volatility across the market as well as a pairwise correlation of 1 between any two of them.

## The True Equilibrium

As more investors become believers in modern portfolio theory along the path towards equilibrium, market continuously updates its view of what the expected return and volatility for each asset should be, until it reaches the point where all of them converge on a single point from a mean-variance standpoint.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier3.svg" />
</div>

## Implications

The comoving condition has profound implications beyond simply everything moving together. Everyday, the god of market draws a random number $r$ out of some unknown distribution, which becomes the market return of the day. At the end of the day,
* every risky asset goes up or down simultaneously by certain amount such that each delivers the same return $r$
* the weights of risky asset remain unchanged indefinitely
* any deviation from such norm will result in either excess demand or supply of certain assets, and thus violates our prerequisite of market equilibrium

Under such condition, covariation with the market will not only become the exclusive systematic risk factor, but the sole source of risk in general as well. The value, size and momentum factors that are prevalent in the market today will not longer deliver excess return. Bearing the market risk fully explains the variation of the return or the risk.

Recall that the market portfolio is meant to be the value-weighted collection of every risky asset, financial or not. How farfetched is it going to be if a condo in San Francisco delivers the same realized return and volatility as, say, Bitcoin? How can the human capital of a Chinese college student respond immediately to, say, the earnings surprise of Apple Inc.? Most importantly, how stable (or unstable in this case) will such equilibrium be before someone realizes something is off?


## Appendix

### Paired Two-sample t-test of return correlation with the market

$$
H_0: \overline{\rho_{before}} - \overline{\rho_{after}} \geq 0\\
H_a: \overline{\rho_{before}} - \overline{\rho_{after}} < 0\\
$$

| t-stat | p-value | degrees of freedom |
| :---: |:---: |:---: |
| -8.1151 | 3.934e-15 | 358 |
