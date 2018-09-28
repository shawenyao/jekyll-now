---
layout: post
title: Black-Scholes-Merton Formula
---

\[S = { S_0 }{ e^{ \left( { r - \frac{ { { \sigma^2 } } }{ 2 }} \right) t + \sigma \sqrt t x}}\]

\[\log S = log{ S_0 } + \left( { r - \frac{ { { \sigma^2} } }{ 2 } } \right)t + \sigma \sqrt t x\]

\[\mu  = log{ S_0 } + \left( {r - \frac{ { { \sigma ^2} } }{ 2 } } \right) t\]

\[\sigma' = \sigma \sqrt t \]

\[{ f_S } \left( S \right) = \frac{ 1 }{ { S\sigma' \sqrt { 2\pi } } }{ e^{ - \frac{ { { { \left( { \log S - \mu } \right) }^2} } }{ { 2 { \sigma' } ^2 } } } }\]

\[{ F_S }\left( S \right) = N \left( { \frac{ { \log S - \mu } }{ { \sigma' } } } \right)\]
