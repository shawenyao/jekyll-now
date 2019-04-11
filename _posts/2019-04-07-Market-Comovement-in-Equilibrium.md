---
layout: post
title: Market Comovement in Equilibrium 
tag:
  - finance
comments: true
draft: true
---

A glimpse of the promised land.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier1.svg" />
</div>

## Introduction

Arguably, one of the most intriguing phenomena of the market is its _dynamism_. Unlike physics where the law of nature is to a large extent independent of human awareness, market responds, adapts and evolves based on what we know about it. For starters, Fama and French's discovery of value and size effect led to a whole new school known as factor investing; likewise, we have never looked at options the same way since Black, Scholes and Merton uncovered the world of geometric Brownian motion; more commonly, arbitrageurs sniff around on a daily basis, exploiting mispricing until it goes way. In all of these instances, it is the knowledge we possess that leads to the action we take, leaving a permanent mark on how market behaves.

One of such curious cases is the modern portfolio theory. Harry Markowitz foresees a world where everybody holds the optimal risky asset. As the separation property states, investors move along the capital allocation line based on their individual risk preferences, holding a combination of the risk-free asset and the tangency portfolio. In equilibrium, the total supply equals the total demand, so the tangency portfolio has to be the value-weighted portfolio of all risky assets - or simply put, the market portfolio.

However, the story doesn't end there. Since the only way in which investors are willing to alter their exposure to risky assets is to adjust their positions in the market portfolio, every order placed on it exerts identical buying (or selling) pressure on all of its constituents. Upon succesful fulfillment of such orders, each constituent's price goes up (or down) by the same amount percentage-wise and the market portfolio remains the value-weighted collection of all risky assets.

A market where everything moves in synchrony presents potential arbitrage opportunities that cannot be sustainable in the long run. It is along these lines that I show in this paper the evidence that the market comovement is stronger than ever, and where it can lead us in equilibrium.

## Empirical Evidence

### Average Asset Correlation: 1960 to 2018

### Index Trading and Return Covariation

Index trading has been more accessible than ever thanks to creation of index fund. Today, three of the most popular S&P 500 index fund are SPY, IVV and VOO.

| Ticker | Name | Inception Date | Asset under Management | Average Daily $ Volume |
| --- | --- | --- | --- | --- |
| SPY | SPDR S&P 500 ETF Trust | Jan 22, 1993 | $272.70B | $17.88B |
| IVV | iShares Core S&P 500 ETF | May 15, 2000 | $175.07B | $1.04B |
| VOO | Vanguard S&P 500 ETF | Sep 7, 2010 | $110.18B | $677.59M |

### Index Constituents and Return Covariation

The S&P 500 index, widely considered to be a proxy of the market portfolio, provides a unique look at how differently an asset would behave upon joining the index trading universe in terms of covariation.

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study1_monthly_rho.svg" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study3_plot3_pre_post_distribution.svg" />
</div>

#### Paired Two-sampe t-test

$$
H_0: \overline{\rho_{before}} - \overline{\rho_{after}} \geq 0\\
H_a: \overline{\rho_{before}} - \overline{\rho_{after}} < 0\\
$$

| t-stat | p-value | degrees of freedom |
| :---: |:---: |:---: |
| -8.1151 | 3.934e-15 | 358 |

## A Comoving Market

### Degeneration of the Efficient Frontier


## Appendix

<div align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study2_monthly_rho_distribution.svg" />
</div>
