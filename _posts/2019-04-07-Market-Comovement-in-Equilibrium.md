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

However, the story does not end there. Since the only way in which investors are willing to alter their exposure to risky assets is to adjust their positions in the market portfolio, every order placed on it exerts identical buying (or selling) pressure on all of its constituents. Upon successful fulfillment of such orders, each constituent's price goes up (or down) by the same amount percentage-wise and the market portfolio remains the value-weighted collection of all risky assets.

A market where everything moves in synchrony presents potential arbitrage opportunities that cannot be sustainable in the long run. It is along these lines that I show in this paper the evidence that the market comovement is stronger than ever, and where it can lead us in equilibrium.

## Index Trading and Return Covariation

The S&P 500 index, widely considered to be a proxy of the market portfolio, provides a unique look at how differently an asset would behave upon joining the index trading universe in terms of covariation. For each of the constituents, we go back to the very date it was included in the index ($t = 0$) and examine its monthly correlation with the index in the preceding year ($-12 \leq t \leq 0$) as well as the subsequent year ($1 \leq t \leq 12$).

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study1_monthly_rho.svg" />
</div>

The difference is small yet significant. The paired two-sample t-test suggests the sheer volume of index trading is strong enough to make a dent in the way the index constituents covary with the index itself. On average, once becoming a constituent, the correlation between the asset and the index rises from 0.458 (as in the year before) to 0.505 (as in the year after).

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study3_pre_post_distribution.svg" />
</div>

## A Comoving Market

The modern portfolio theory states that under the homogenous expectations assumption, every investor has the same view when it comes to estimating the expected return, volatility and correlation of all risky assets. Every investor then goes ahead and solves for the same mean-variance optimization problem and arrives at the same answer - the efficient frontier.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier1.svg" />
</div>

The limiting case of the S&P 500 index trading example will lead us to something fairly similar to Harry Markowitz's conceptual world of equilibrium, where
* every investor only holds the market portfolio
* every transaction is done via trading the market portfolio

As mentioned earlier, the fact that market portfolio becomes the only trading vehicle will consequently make all individual risky assets that the market is composed of go up and down in price as one, implying a pairwise correlation of 1.

### Degeneration of the Efficient Frontier

Holding everything else constant, we plug in the condition that every pairwise correlation equals to 1. As long as there are at least two risky assets on the market, volatility can be completely diversified away by going long in one and short in the other with the appropriate weighting scheme. Should the resulting zero-volatility portfolio have an expected return not the same as the risk-free rate, the efficient frontier reduces to a vertical line at volatility equals to 0.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier2.svg" />
</div>

If the efficient frontier in such form looks unorthodox, that's because it is too good to be true. As it stands, at least two zero-volatility assets (the true risk-free asset and the synthetic one) coexist. Any possible return can be promised by borrowing at the lower "risk-free" rate and investing at the higher one, with absolute zero uncertainty. The presence of guaranteed, risk-free and profitable arbitrage opportunity violates our premise of a market in equilibrium.

### The True Equilibrium

Fortunately, market always finds a way to restore balance, by virtue of the collective efforts from the rational, diligent and profit-seeking investors. As with all arbitrage opportunities, exploiting them will cause them to diminish and eventually disappear. Price of overvalued assets will decrease, implying a higher expected return in the future so that people are going to be willing to hold them in their portfolios again; on the other hand, price of undervalued assets will rise and people will no longer find them as attractive and thus decide to reduce their holdings. 

Along the path towards the new equilibrium, market continuously updates the view of what the expected return and volatility for each asset should be, until it reaches the point where all of them align on a straight line that begins from the risk-free asset:

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier3.svg" />
</div>

Or equivalently, all assets will have the same Sharpe ratio:

$$
Sharpe\ Ratio = \frac{ E(r) - r_f }{ \sigma }
$$

As such, despite all risky assets still being perfectly correlated, any zero-volatility portfolio synthesized this way will by design have the same expected return as the risk-free rate. At this point, every risky asset is a fair game from a mean-variance optimization standpoint, but investors will continue to hold them through (and only through) holding the market portfolio. This is the only form in which the market reaches the state of equilibrium while staying arbitrage-free.

### Implications

## Conculsions

## Appendix

### Paired Two-sampe t-test

$$
H_0: \overline{\rho_{before}} - \overline{\rho_{after}} \geq 0\\
H_a: \overline{\rho_{before}} - \overline{\rho_{after}} < 0\\
$$

| t-stat | p-value | degrees of freedom |
| :---: |:---: |:---: |
| -8.1151 | 3.934e-15 | 358 |
