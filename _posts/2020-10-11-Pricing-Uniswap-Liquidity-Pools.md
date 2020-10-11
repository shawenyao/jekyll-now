---
layout: post
title: Pricing Uniswap Liquidity Pools
tag:
  - defi
  - finance
  - maths
comments: true
draft: true
finance: true
---
DeFi or CeFi?

Just like how Bitcoin aims to revolutionize money, automated market maker (AMM) emerges the disruptor of tranditional exchange. 

At the time of writing, Uniswap, the biggest decentralized finance (DeFi) protocols, have over $2.5 billion in total value locked in its liquidity pool according to [DeFi Pulse](https://defipulse.com/).

## Uniswap Explained

$$ a_T b_T = k $$

This is known as the constant product formula.

$$ a_T b_T = k + \sum_{t=0}{T} f_t $$

## Problem Formulation

Examine the liquidity composed of asset $A$ and $B$. Define the price of one unit of asset $A$ in terms of one unit of asset $B$ as:

$$ p_T = \frac{ A_T }{ B_T } $$

How much is the liquidity pool worth today if the liquidity provider puts down equal value of $A$ and $B$ into the pool now?

Note that the following analysis is based on the assumption of zero liquidity pool growth (other than due to transaction fees).

## Pricing

For simplicity, let $a_T$ and $b_T$ denote the number of units of $A$ and $B$ in the liqudity pool respectively. For the two assets to have equal value at any point in time, we have:

$$ a_T p_T = b_T $$


## What about Transaction Fees?
In other words, transaction fees in its current form bring _path dependence_ into the equation.

## Conclusions

## Appendix
