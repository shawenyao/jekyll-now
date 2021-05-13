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

## A Closer Look

<div align="center">
  <img src="https://shawenyao.github.io/R/output/uniswap_vs_exchange/plot3_uniswap_vs_exchange_distribution.png" />
</div>


| pair | mean | sd | t |
|---|---|---|---|
| BTC-ETH | 0.0004 | 0.0045 | 0.0916 |
| USDT-ETH | -0.0004 | 0.0053 | -0.0767 |
| USDC-ETH | -0.0002 | 0.0319 | -0.0070 |
| DAI-ETH | 0.0002 | 0.0055 | 0.03930 |
| USDC-USDT | 0.0009 | 0.0035 | 0.2540 |


This could be partially explained by the fact the USDC-USDT pool is the worst funded one of them all.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/uniswap_vs_exchange/plot4_uniswap_vs_exchange_reserve.png" />
</div>

## Conclusions

## Appendix

Sample query: the historical liquidity pool balances of the BTC/ETH pair on Uniswap (powered by the [Graph](https://thegraph.com/explorer/subgraph/uniswap/uniswap-v2))

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
