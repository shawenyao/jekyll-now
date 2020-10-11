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

$$ p_t = \frac{ A_t }{ B_t } = \frac{ b_t }{ a_t } $$

At time $0$, there are $a_0$ units of asset $A$ and $b_0$ units of asset $B$ in the pool. Now, if a new order comes along to buy $\Delta a_1$ units of asset $B$, after the transaction fullfills, the ending balances in the pool for asset $A$ and $B$ will be:

$$ a_1 = a_0 - \Delta a_1 $$

$$ b_1 = \frac{ k }{ a_0 - \Delta a_1 } $$

This implies a new price of:

$$ p_1 = \frac{ a_0 b_0 }{ (a_0 - \Delta a_1)^2 } = \frac{ a_0^2 }{ (a_0 - \Delta a_1)^2 } \cdot \frac{ b_0 }{ a_0 } > \frac{ b_0 }{ a_0 } = p_0 $$

which indicates that asset $A$ has appreciated against asset $B$, as a result of having fulfilled the demand for asset $A$ and the subsequent "scarcity" of it in the pool. This setup has a few desirable properties to it. To name a few:
* if there's no trade, the price level stays at its initial value
* a smaller trade is expected to be fullfiled at the market price without moving it by much
* a larger trade will move the price substantially along the hyperbolic curve, deterioating the price level
* a very large trade (e.g., something close to the remaining balance in the pool) will lead to a price impact so prohibitively substantial that it is close to impossible to deplete the inventory.

In other words, Uniswap appears to achieve _infinite_ market depth with _finite_ supply of assets.

## Problem Formulation
How much is the liquidity pool worth today if the liquidity provider puts down equal value of $A$ and $B$ into the pool now?

Note that the following analysis is based on the assumption of zero liquidity pool growth (other than due to transaction fees). Also the risk-free rate is assumed to be 0.

## Price Slippage vs Fee Income
The payoff at time $t$ for liquidity providers consists of two parts - loss due to price slippage and income from collecting transaction fees. 

One on hand, as transactions happen, newly fulfilled supply or demand drives the price away from its starting point, otherwise known as price slippage. Unfortunately, price slippage always incurs loss(to see why, see appendix). To compensate for this, every transaction fulfilled by AMM charges a fee. For example, Uniswap charges 0.3% to all trades. The fees are put back to the pool immediately after collection and every liquidity provider has a pro rata claim on them. As it stands, fee income is effectively the sole incentivie for liquidity providers to contribute assets into the pool.

The introduction of transaction fees brings _path dependence_ into the equation. Depending on how many orders (and how big the order size is) have been fulfilled, liquidity providers might or might not be able to make a profit on their investment. This requires a slight modification to the constant production formula introduced earlier,

$$ a_t b_t = k + \sum_{i=1}^{t} f_i $$

where $f_i$ is the amount of transaction fees collected at time $i$.

## Conclusions


## References
Uniswap. 2020. "[How Uniswap works](https://uniswap.org/docs/v2/protocol-overview/how-uniswap-works/)"

Pintail. 2020. "[Uniswap: A Good Deal for Liquidity Providers?](https://medium.com/@pintail/uniswap-a-good-deal-for-liquidity-providers-104c0b6816f2)"

AlfaBlok. 2019. "[Risk/Reward of liquidity provision in AMMs](https://alfablok.substack.com/p/coming-soon)"

## Appendix
### The Effect of Price Slippage

In the absence of transaction fees, compare the terminal values of the two following strategies:
* strategy 1: buy and hold
* strategy 2: stake in liquidity pool

Strategy 1's terminal value is given by:

$$\begin{align}
v_t &= a_0 p_t + b_0 \\
 % &= a_0 \frac{ b_t }{ a_t }  + b_0 \\
 % &= a_0 \frac{ \frac{ k }{ a_t } }{ a_t } + b_0 \\
 % &= a_0 \frac{ \frac{ a_0 b_0 }{ a_t } }{ a_t } + b_0 \\
 &= (\frac{ a_0 ^ 2 }{ a_t^2 } + 1) b_0
\end{align}$$

Meanwhile, strategy 2 will have a terminal value of:

$$\begin{align}
v'_t &= a_t p_t + b_t \\
 % &= a_t \frac{ b_t }{ a_t } + b_t \\
 % &= 2b_t \\
 % &= 2 \frac{ k }{ a_t } \\
 &= \frac{ 2 a_0 b_0 }{ a_t } \\
\end{align}$$

Divide $v_t$ by $v'_t$, 

$$\begin{align}
\frac{ v_t }{ v'_t } &= \frac{ \frac{ a_0 ^ 2 }{ a_t^2 } + 1 }{ \frac{ 2a_0 }{ a_t } } \\
 % &= \frac{ \frac{ a_0 }{ a_t } + \frac{ a_t }{ a_0 } }{ 2 } \\
 % &= \frac{ a_0^2 + a_t^2 }{ 2 a_0 a_t } \\
 % &= \frac{ (a_0 - a_t)^2 + 2 a_0 a_t }{ 2 a_0 a_t } \\
 &= \frac{ (a_0 - a_t)^2 }{ 2 a_0 a_t } + 1 \\
 &\geq 1
\end{align}$$

As a result, price slippage always results in lower terminal value, i.e., a loss from liquidity providers' standpoint.
