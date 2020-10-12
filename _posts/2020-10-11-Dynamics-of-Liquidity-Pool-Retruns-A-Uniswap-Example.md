---
layout: post
title: Dynamics of Liquidity Pool Returns&#58 A Uniswap Example
tag:
  - defi
  - finance
  - maths
comments: true
draft: true
finance: true
---
DeFi or CeFi?

Just like how Bitcoin aims to revolutionize money, automated market maker (AMM) emerges as the disruptor of tranditional exchange. While NYSE and Nasdaq use an order book for price discovery, Uniswap, the biggest decentrailized exchange, relies on what's known as the constant product formula.

At the time of writing, Uniswap has over $2.5 billion in total value locked in its liquidity pool according to [DeFi Pulse](https://defipulse.com/).

Note that the following analysis is based on the assumption of zero liquidity pool growth (other than due to transaction fees). Also, the risk-free rate is assumed to be 0.

## Uniswap Explained

Uniswap divides its market participants into two categories: liquidity providers and traders. In a nutshell, the former deposits equal value of any pair of assets into the liquidity pool and the latter trades one for the other based on what's available in the pool.

Examine the liquidity pool composed of asset $A$ and $B$. For simplicity, let $a_t$ and $b_t$ denote the number of units of $A$ and $B$ available in the liqudity pool respectively. At any point in time, we have:

$$ a_t b_t = k $$

This is known as the constant product formula. Since the liquidity pool have equal value of both assets, it also implies that the current exchange rate of one unit of asset $A$ in terms asset $B$ is

$$ e_t = \frac{ A_t }{ B_t } = \frac{ b_t }{ a_t } $$

where $A_t$ and $B_t$ are the unit prices of asset $A$ and $B$ measured in a common numeraire (be it Bitcoin or US dollar, your choice).

At time $0$, there are $a_0$ units of asset $A$ and $b_0$ units of asset $B$ in the pool. Now, if a new order comes along to buy $\Delta a_1$ units of asset $A$, after the transaction settles, the ending balances in the pool for asset $A$ and $B$ will be:

$$ a_1 = a_0 - \Delta a_1 $$

$$ b_1 = \frac{ k }{ a_0 - \Delta a_1 } $$

This implies a new exchange rate of:

$$ e_1 = \frac{ a_0 b_0 }{ (a_0 - \Delta a_1)^2 } = \frac{ a_0^2 }{ (a_0 - \Delta a_1)^2 } \cdot \frac{ b_0 }{ a_0 } > \frac{ b_0 }{ a_0 } = e_0 $$

which indicates that asset $A$ has appreciated against asset $B$, as a result of having fulfilled the demand for asset $A$ and the subsequent "scarcity" of it in the pool.

While the individual prices of asset $A$ and $B$ can still very much follow their own dynamics, Uniswap provides a way for traders to express their view on the price of one in terms of the other. In other words, everything is being valued on a relative term in the Uniswap exchange. This setup has a few desirable properties to it - to name a few:
* if there's no trade, the price level stays at its initial value
* a smaller trade is expected to be fullfiled at the market price without moving it by much
* a larger trade will move the price substantially along the hyperbolic curve, with the asset in demand appreciating against the other
* a very large trade (e.g., something close to the remaining balance in the pool) will lead to a price impact so prohibitively substantial that it is close to impossible to deplete the inventory.

In other words, Uniswap appears to achieve _infinite_ market depth with _finite_ supply of assets. Putting it all together, the liquidity provider puts down:

$$ v_0 = a_0 A_0 + b_0 B_0 $$

amount of money (again, measured in an arbitrary numeraire) today in exchange for:

$$ v_t = a_t A_t + b_t B_t $$

at time $t$. 

## Price Slippage vs Fee Income
The payoff at time $t$ for liquidity providers consists of two parts - capital appreciation (or depreciation) due to price slippage and income from collecting transaction fees. 

One on hand, as trades fulfill, newly-arrived supply and demand drive the price away from its starting point. Formerly known as price slippage, this phenomenon can lead to either a gain or loss to the liquidity provider, but it always underforms a buy and hold strategy (to see why, see appendix). To compensate for the underperformance, AMM usually charges a fee for trading. For example, Uniswap collects 0.3% on every transaction. The fees are put back to the pool right away and every liquidity provider has a pro rata claim on them. As it stands, fee income is effectively the sole incentivie for liquidity providers to contribute assets into the pool, compared to simply holding on to the asset pair.

The introduction of transaction fees brings _path dependence_ into the equation. The terminal state alone is no longer sufficient to uniquely determine the payoff to liquidity provider - the path through which it arrives at the ending price also matters. This requires a slight modification to the constant production formula introduced earlier:

$$ a_t b_t = a_{ t-1 } b_{ t-1 } + f_t $$

where $f_t$ is the amount of transaction fees collected at time $t$.

## Simulation

Assume the prices of asset $A$ and $B$ follow the following dynamics:

$$
\frac{ dA_t }{ A_t } = \mu^A dt + \sigma^A dW^A \\
\frac{ dB_t }{ B_t } = \mu^B dt + \sigma^B dW^B \\
$$

where $dW^A$ and $dW^B$ are correlated Brownian motions:

$$ dW^A dW^B = \rho dt $$

Ignorning fees, the new price pair $A_t$ and $B_t$ defines how the pool evolves from the previous point:

$$
\begin{cases}
\frac{ A_t }{ B_t } = \frac{ b'_t }{ a'_t } \\ 
a'_t b'_t = a_{ t-1 } b_{ t-1 } \\
\end{cases}
$$

which yields:

$$
\begin{cases}
a'_t = \sqrt{ \frac{ a_{ t-1 } b_{ t-1 } A_t }{ B_t } } \\ 
b'_t = \sqrt{ \frac{ a_{ t-1 } b_{ t-1 } B_t }{ A_t } } \\
\end{cases}
$$

After taking transaction fees into consideration, we have the final form of remaining balances in the liquidity pool:

$$
\begin{cases}
a_t = a'_t + \textbf{ 1 }_{ a_{ t-1 } \geq a'_t } ( a_{ t-1 } - a'_t ) c \\ 
b_t = b'_t + \textbf{ 1 }_{ a_{ t-1 } < a'_t } ( b_{ t-1 } - b'_t ) c \\ 
\end{cases}
$$

where $c$ is the transaction fee rate and  $\textbf{ 1 }$ is the indicator function that takes the value of 1 if the underlying condition is true, or 0 if otherwise. Depending whether the order is to buy asset $A$ with asset $B$ or vice versa, transaction fees can either take the form of asset $A$ or $B$ before being put back to the liquidity pool. More specifically, 
* if $a_{ t-1 }$ is greater than $a'_t$, the trader must have purchased asset $A$ with asset $B$, resulting in a decline in the balance of asset $A$. The protocol retains a portion of the payout (asset $A$) as transaction fees.
* if $a_{ t-1 }$ is less than $a'_t$, the trader must have purchased asset $B$ with asset $A$, resulting in an increase in the balance of asset $B$. The protocol retains a portion of the payout (asset $B$) as transaction fees.

## Conclusions


## References
Uniswap. 2020. "[How Uniswap works](https://uniswap.org/docs/v2/protocol-overview/how-uniswap-works/)"

Pintail. 2020. "[Uniswap: A Good Deal for Liquidity Providers?](https://medium.com/@pintail/uniswap-a-good-deal-for-liquidity-providers-104c0b6816f2)"

AlfaBlok. 2019. "[Risk/Reward of liquidity provision in AMMs](https://alfablok.substack.com/p/coming-soon)"

## Appendix
### The Effect of Price Slippage

In the absence of transaction fees, compare the terminal values of the two following strategies:
* strategy X: buy and hold
* strategy Y: contribute to liquidity pool

Strategy X's terminal value is given by:

$$\begin{align}
v_t^X &= (a_0 e_t + b_0) B_t \\
 % &= (a_0 \frac{ b_t }{ a_t }  + b_0) B_t \\
 % &= (a_0 \frac{ \frac{ k }{ a_t } }{ a_t } + b_0) B_t \\
 % &= (a_0 \frac{ \frac{ a_0 b_0 }{ a_t } }{ a_t } + b_0) B_t \\
 &= (\frac{ a_0 ^ 2 }{ a_t^2 } + 1) b_0 B_t
\end{align}$$

Meanwhile, strategy Y will have a terminal value of:

$$\begin{align}
v_t^Y &= (a_t e_t + b_t) B_t \\
 % &= (a_t \frac{ b_t }{ a_t } + b_t) B_t \\
 % &= 2b_t B_t \\
 % &= 2 \frac{ k B_t }{ a_t } \\
 &= \frac{ 2 a_0 b_0 B_t }{ a_t } \\
\end{align}$$

Divide $v_t^1$ by $v_t^2$, 

$$\begin{align}
\frac{ v_t^X }{ v_t^Y } &= \frac{ \frac{ a_0 ^ 2 }{ a_t^2 } + 1 }{ \frac{ 2a_0 }{ a_t } } \\
 % &= \frac{ \frac{ a_0 }{ a_t } + \frac{ a_t }{ a_0 } }{ 2 } \\
 % &= \frac{ a_0^2 + a_t^2 }{ 2 a_0 a_t } \\
 % &= \frac{ (a_0 - a_t)^2 + 2 a_0 a_t }{ 2 a_0 a_t } \\
 &= \frac{ (a_0 - a_t)^2 }{ 2 a_0 a_t } + 1 \\
 &\geq 1
\end{align}$$

As a result, a buy and hold strategy always outperforms being a liquidity provider in the absence of fee income.
