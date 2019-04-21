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

The modern porfolio theory states that under the homogenous expectations assumption, every investor has the same view when it comes to estimating the expected return, volatility and correlation of all risky assets. Every investor then goes ahead and solves for the same mean-variance optimization problem and arrvies at the same answer - the efficient frontier.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier1.svg" />
</div>

The limiting case of the S&P 500 index trading example will lead us to something fairly similar to Harry Markowitz's conceptual world of equilibirm, where
* every investor only holds the market portfolio
* every transaction is done via trading the market potfolio

As mentioned earlier, the fact that market portfolio becomes the only trading vehicle will consequently make all individual risky assets that the market is composed of go up and down in price as one, implying a pairwise correlation of 1.

### Degeneration of the Efficient Frontier

Holding everything else constant, we plug in the condition that every pairwise correlation equals to 1. As long as there are at least two risky assets on the market, volatility can be completely diversified away by going long in one and short in the other with the appropriate weighting scheme. Should the resulting zero-volatility portfolio have an expected return not the same as the risk-free rate, the efficient frontier degenrates to a vertical line at volatility equals to 0.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier2.svg" />
</div>

If the efficent frontier in such form looks unorthodox, that's because it is too good to be true. As it stands, at least two zero-volatility assets (the true risk-free asset and the synthetic one) coexist. Any possible return can be promised by borrowing at the lower "risk-free" rate and investing at the higher one, with abosulte zero uncertainty. The presence of guaranteed, risk-free and profitable arbitrage opportunity violates our premise of a market in equilibrum.

### A Market in Synchrony

Fortunately, market always finds a way to bring balance back, by virtue of the collective efforts from the rational, diligent and profit-seeking investors. As with all arbitrage opportunities, exploiting them will casue them to diminish and eventually disappear. Price of overvalued assets will decrease, implying a higher expected return in the future so that people will be willing to hold them in their portfolios again; on the other hand, price of undervalued assets will rise to the point where people no longer find them as attractive and decide to reduce their holdings. 

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier3.svg" />
</div>

This is the only form in which the market reaches tha state of equilibrium while staying arbitrage-free.

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
