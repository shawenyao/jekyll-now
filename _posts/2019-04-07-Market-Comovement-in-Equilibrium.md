---
layout: post
title: Market Comovement in Equilibrium 
tag:
  - finance
comments: true
draft: true
---

A glimpse of the promised land.

## Introduction

Arguably, one of the most intriguing phenomena of the market is its _dynamism_. Unlike physics where the law of nature is to a large extent independent of human awareness, market responds, adapts and evolves based on what we know about it. For starters, Fama and French's discovery of value and size effect led to a whole new school known as factor investing; likewise, we have never looked at options the same way since Black, Scholes and Merton uncovered the world of geometric Brownian motion; more commonly, arbitrageurs sniff around on a daily basis, exploiting mispricing until it goes way. In all of these instances, it is the knowledge we possess that leads to the action we take, leaving a permanent mark on how market behaves.

One of such curious cases is the modern portfolio theory. Harry Markowitz foresees a world where everybody holds the optimal risky asset. As the separation property states, investors move along the capital allocation line based on their individual risk preferences, holding a combination of the risk-free asset and the tangency portfolio. In equilibrium, the total supply equals the total demand, so the tangency portfolio has to be the value-weighted portfolio of all risky assets - or simply put, the market portfolio.

However, the story doesn't end there. Since the only way in which investors are willing to alter their exposure to risky assets is to adjust their positions in the market portfolio, every order placed on it exerts identical buying (or selling) pressure on all of its constituents. Upon succesful fulfillment of such orders, each constituent's price goes up (or down) by the same amount percentage-wise and the market portfolio remains the value-weighted collection of all risky assets.

A market where everything moves in synchrony presents potential arbitrage opportunities that cannot be sustainable in the long run. It is along these lines that I show in this paper the evidence that the market comovement is stronger than ever, and where it can lead us in equilibrium.

## Empirical Evidence

### Index Trading and Return Covariation

Index trading has been more accessible than ever since the creation of index fund. Today, three of the most popular S&P 500 index fund are SPY, IVV and VOO.

| Ticker | Name | Inception Date | Asset under Management | Average Daily $ Volume |
| --- | --- | --- | --- | --- |
| SPY | SPDR S&P 500 ETF Trust | Jan 22, 1993 | $272.70B | $17.88B |
| IVV | iShares Core S&P 500 ETF | May 15, 2000 | $175.07B | $1.04B |
| VOO | Vanguard S&P 500 ETF | Sep 7, 2010 | $110.18B | $677.59M |

Suppose we want to examine the linear relationship between the monthly average index correlation and the combined monthly ETF dollar volume:

$$
\overline{\rho_{index}} = \beta_0 + \beta_1 DV + \epsilon
$$

where the average index correlation is defined as:

$$
\overline{\rho_{index}} = \frac{ 1 }{ (N-1) N / 2 } \displaystyle \sum_{ i<j } \rho_{ij}
$$

### Index Constituents and Return Covariation

The S&P 500 index, widely considered to be a proxy of the market portfolio, provides a unique look at how differently an asset would behave upon joining the index trading universe in terms of covariation. For each of the constitunets, we go back to the very date it was included in the index ($t = 0$) and examine its monthly correlation with the index in the preceding year ($-12 \leq t \leq 0$) as well as the subsequent year ($1 \leq t \leq 12$).

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study1_monthly_rho.svg" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study3_plot3_pre_post_distribution.svg" />
</div>

The difference is small yet siginificant. The paired two-sampe t-test suggests the sheer volume of index trading is strong enough to make a dent in the way the index constituents covary with the index itself. On average, once becoming a constituent, the correlation between the asset and the index rises from 0.458 (as in the year before) to 0.505 (as in the year after).

## A Comoving Market

What if we take the S&P 500 index trading case to the extreme? It is not inconeivable that we will be looking at something fairly similar to Harry Markowitz's conceptual world of equilibirm where
* every investor only holds the market portfolio
* all transactions is done via trading the market potfolio

As mentioned earlier, the fact that market portfolio becomes the only trading vehicle will consequently make all individual risky assets that the market is composed of go up and down in price as one, implying a pairwise correlation of 1.

### Degeneration of the Efficient Frontier

As the model porfolio theory states, under the homogenous expectations assumption, every investor has the same view when it comes to estimating the expected return, volatility and correlation of all risky assets. Every investor then goes ahead and solves for the same mean-variance optimization problem and arrvies at the same answer - the efficient frontier.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier1.svg" />
</div>

Holding everything else constant, we plug in the condition that every pairwise correlation equals to 1. As long as there are at least two assets with different expected returns, volatility can be completely eliminated by going long in one and short in the other. Should the difference in their expected returns be not the same as the risk-free rate, the efficient frontier degenrates to a vertical line at volatility equals to 0.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier2.svg" />
</div>

If the efficent frontier in such form looks unorthodox, that's because it is.

## Appendix

### Paired Two-sampe t-test

$$
H_0: \overline{\rho_{before}} - \overline{\rho_{after}} \geq 0\\
H_a: \overline{\rho_{before}} - \overline{\rho_{after}} < 0\\
$$

| t-stat | p-value | degrees of freedom |
| :---: |:---: |:---: |
| -8.1151 | 3.934e-15 | 358 |

### The Evolution of Average Monthly Correlation

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study2_monthly_rho_distribution.svg" />
</div>
