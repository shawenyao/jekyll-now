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

Examine the liquidity composed of asset $A$ and $B$.

For simplicity, let $a_t$ and $b_t$ denote the number of units of $A$ and $B$ available in the liqudity pool respectively. At any point in time, we have:

$$ a_t b_t = k $$

This is known as the constant product formula. It also implies that the current price of one unit of asset $A$ in terms asset $B$ is

$$ p_t = \frac{ A_t }{ B_t } $$ = \frac{ b_t }{ a_t }

## Problem Formulation
How much is the liquidity pool worth today if the liquidity provider puts down equal value of $A$ and $B$ into the pool now?

Note that the following analysis is based on the assumption of zero liquidity pool growth (other than due to transaction fees). Also the risk-free rate is assumed to be 0.

## Pricing
Price slippage always incurs loss for the liquidity provider (to see why, see appendix).

For the two assets to have equal value at any point in time, we have:

$$ a_t p_t = b_t $$

## What about Transaction Fees?
In practice, every transaction fulfilled by AMM incurs a fee. For example, Uniswap charges 0.3% to all trades. The 

In other words, transaction fees in its current form bring _path dependence_ into the equation. This requires a slight modification to the constant production formula introduced earlier, n

$$ a_t b_t = k + \sum_{i=1}^{N_t} f_i $$

where $N_t$ is the total number of traders that has happened from time $0$ to time $t$.

## Conclusions


## References
Uniswap, "[How Uniswap works](https://uniswap.org/docs/v2/protocol-overview/how-uniswap-works/)"

Pintail, "[Uniswap: A Good Deal for Liquidity Providers?](https://medium.com/@pintail/uniswap-a-good-deal-for-liquidity-providers-104c0b6816f2)"

AlfaBlok, "[Risk/Reward of liquidity provision in AMMs](https://alfablok.substack.com/p/coming-soon)"

## Appendix
### The Effect of Price Slippage

In the absence of transaction fees, compare the terminal values of the two following strategies.
* strategy 1: buy and hold
* strategy 2: stake in liquidity pool

Strategy 1's terminal value is given by:

$$\begin{align}
v_t &= a_0 p_t + b_0 \\
 &= a_0 \frac{ b_t }{ a_t }  + b_0 \\
 &= a_0 \frac{ \frac{ k }{ a_t } }{ a_t } + b_0 \\
 &= a_0 \frac{ \frac{ a_0 b_0 }{ a_t } }{ a_t } + b_0 \\
 &= (\frac{ a_0 ^ 2 }{ a_t^2 } + 1) b_0
\end{align}$$

Meanwhile, strategy 2 will have a terminal value of:

$$\begin{align}
v'_t &= a_t p_t + b_t \\
 &= a_t \frac{ b_t }{ a_t } + b_t \\
 &= 2b_t \\
 &= 2 \frac{ k }{ a_t } \\
 &= 2 \frac{ a_0 b_0 }{ a_t } \\
\end{align}$$

Divide $v_t$ by $v'_t$, 

$$\begin{align}
\frac{ v_t }{ v'_t } &= \frac{ \frac{ a_0 ^ 2 }{ a_t^2 } + 1 }{ \frac{ 2a_0 }{ a_t } } \\
 &= \frac{ \frac{ a_0 }{ a_t } + \frac{ a_t }{ a_0 } }{ 2 } \\
 & = 2b_t \\
\end{align}$$
