---
layout: post
title: Market Comovement in Equilibrium 
tag:
  - finance
comments: true
draft: true
---

A glimpse of the promised land.

<p align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/efficient_frontier1.svg" />
</p>

## Introduction

Arguably, one of the most intriguing phenomena of the market is its _dynamism_. Unlike physics where the law of nature is to a large extent independent of human awarness, market responds, adapts and evolves based on what we know about it. For starters, Fama and French's discovery of value and size effect led to a whole new school known as factor investing; likewise, we have never looked at options the same way since Black, Scholes and Merton uncovered the world of geometric Brownian motion; more commonly, arbitrageurs sniff around on a daily basis, exploiting mispricing until it goes way. In all of these instances, it is the knowledge we possess that leads to the action we take, leaving a permanent mark on how market behaves.

One of such curious cases is the modern portfolio theory. Harry Markowitz foresees a world where everybody holds the optimal risky asset. As the separation property states, investors move along the capital allocation line based on their individual risk preferences, holding a combination of the risk-free asset and the tangency portfolio. In equilibrium, the total supply equals the total demand, so the tangency portfolio has to be the value-weighted portfolio of all risky assets - or simply put, the market portfolio.

However, the story doesn't end there. Since the only way in which investors are willing to alter their exposure to risky assets is to adjust their positions in the market portfolio, every order placed on the market portfolio exerts equal buying or selling pressure on all of its constituents. Upon succesful fulfillment of such orders, each constituent's price goes up or down by identical amount percentage-wise, and the market portfolio remains the value-weighted set of all risky assets.

A market where everything moves homogeneously presents tremendous arbitrage opportunities that cannot be sustainable in the long run. In this paper, I present evidence that the market is behaving increasingly along the lines that Harry Markowitz foretold, and where that leads in equilibrium.

## Empirical Evidence

<p align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study1_monthly_rho.svg" />
</p>

<p align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study2_monthly_rho_distribution.svg" />
</p>

<p align="center">
  <img src="https://shawenyao.github.io/ETF-vs-rho/output/event_study3_plot3_pre_post_distribution.svg" />
</p>