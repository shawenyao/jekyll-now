---
layout: post
title: Price Efficiency on Uniswap
tag:
  - defi
  - finance
comments: true
draft: true
finance: true
new: true
---
Constant product formula vs. order book.

In the previous [post](/Dynamics-of-Liquidity-Pool-Returns-A-Uniswap-Example/), we discussed the way by which an automated market maker (AMM) such as Uniswap determines market price. The fundamental mechanism underlying the decentralized exchange is known as the constant product formula, which states that given a certain supply of asset X and Y in the liqudity pool, the product of their outstanding balances should be a constant. This differs drastically from how traditional electronic exchanges such as NYSE, NASDAQ or even Coinbase functions.

Obviously, the law of one price dictates that the two cannot be too far apart. Otherwise, it creates actionable arbitrage opportunity if the spread is wide enough to remain positive on an after-transaction-cost basis.

## Data Feeds

## Price Discovery: Uniswap vs Exchange

<div align="center">
  <img src="https://shawenyao.github.io/R/output/uniswap_vs_exchange/plot1_uniswap_vs_exchange.png" />
</div>

The divergence is more clearly visible on a difference % scale:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/uniswap_vs_exchange/plot2_uniswap_vs_exchange_diff.png" />
</div>

For most of the time, the price ratio on Uniswap is well within 1% of the "actual" value, i.e., the one quoted on order-book-style exchanges.

## A Closer Look

<div align="center">
  <img src="https://shawenyao.github.io/R/output/uniswap_vs_exchange/plot3_uniswap_vs_exchange_distribution.png" />
</div>

This could be partially explained by the fact the USDC-USDT pool is the worst funded one of them all.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/uniswap_vs_exchange/plot4_uniswap_vs_exchange_reserve.png" />
</div>

## Conclusions

## Appendix

### Summary Statistics: 

Price ratio difference %:

| pair | mean | sd | t |
|---|---|---|---|
| BTC-ETH | 0.04% | 0.0045 | 0.0916 |
| USDT-ETH | -0.04% | 0.0053 | -0.0767 |
| USDC-ETH | -0.02% | 0.0319 | -0.0070 |
| DAI-ETH | 0.02% | 0.0055 | 0.03930 |
| USDC-USDT | 0.09% | 0.0035 | 0.2540 |

### Sample Query

The historical liquidity pool balances of the BTC/ETH pair on Uniswap (powered by the [Graph](https://thegraph.com/explorer/subgraph/uniswap/uniswap-v2)):

```json
{
  pairDayDatas(
    first: 1000,
    orderBy: date, 
    orderDirection: desc, 
    where: { 
      pairAddress: "0xbb2b8038a1640196fbe3e38816f3e67cba72d940"
    }
  ){
    id 
    date 
    token0
    { id symbol } 
    token1
    { id symbol } 
    reserve0,
    reserve1,
    reserveUSD,
    dailyVolumeUSD
  } 
}
```
