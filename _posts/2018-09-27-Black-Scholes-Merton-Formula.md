---
layout: post
title: Black-Scholes-Merton Formula
tags:
 - maths
 - finance
---

A step-by-step derivation.

Given that:

$$ S = { S_0 }{ e^{ \left( { r - \frac{ { { \sigma^2 } } }{ 2 }} \right) t + \sigma \sqrt t x}} $$

where

$$x \sim N(0,1)$$

we have:

$$ \log S = \log{ S_0 } + \left( { r - \frac{ { { \sigma^2} } }{ 2 } } \right)t + \sigma \sqrt t x $$

Let 

$$ \mu  = \log{ S_0 } + \left( {r - \frac{ { { \sigma ^2} } }{ 2 } } \right) t $$ 

$$ \sigma' = \sigma \sqrt t $$

the probability desnity function $f_S(S)$ and cumulative distribution function $F_S(S)$ can be written as:

$$ { f_S } \left( S \right) = \frac{ 1 }{ { S\sigma' \sqrt { 2\pi } } }{ e^{ - \frac{ { { { \left( { \log S - \mu } \right) }^2} } }{ { 2 { \sigma' } ^2 } } } } $$

$$ { F_S }\left( S \right) = N \left( { \frac{ { \log S - \mu } }{ { \sigma' } } } \right) $$

Consider the value of a vanilla European call option:

$$\begin{align}
\mathbb{ E^Q }\left[ { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  } } \right]
 &= \int\limits_{  - \infty  }^{  + \infty  } { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  }{ f_S }\left( S \right)dS } \\
 &= \int\limits_{  - \infty  }^K { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  }{ f_S }\left( S \right)dS }  + \int\limits_K^{  + \infty  } { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  }{ f_S }\left( S \right)dS } \\
 &= \int\limits_K^{  + \infty  } { { e^{  - rt } }\left( { S - K } \right){ f_S }\left( S \right)dS } \\
 &= \int\limits_K^{  + \infty  } { { e^{  - rt } }S{ f_S }\left( S \right)dS }  - \int\limits_K^{  + \infty  } { { e^{  - rt } }K{ f_S }\left( S \right)dS } \\
 &= { e^{  - rt } }\int\limits_K^{  + \infty  } { S{ f_S }\left( S \right)dS }  - K{ e^{  - rt } }\int\limits_K^{  + \infty  } { { f_S }\left( S \right)dS } 
\end{align}$$

The first term:

$$\begin{align}
{ e^{  - rt } }\int\limits_K^{  + \infty  } { S{ f_S }\left( S \right)dS }
 &= { e^{  - rt } }\int\limits_K^{  + \infty  } { S\frac{ 1 }{ { S\sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { \log S - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }dS } \\
 &= { e^{  - rt } }\int\limits_K^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { \log S - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }dS } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { y - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }d\left( { { e^y } } \right) } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ { { e^y } } }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { y - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { y - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } + y } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left( { { y^2 } - 2y\mu  + { \mu ^2 } - 2\sigma { '^2 }y } \right) } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { y^2 } - \left( { 2\mu  + 2\sigma { '^2 } } \right)y + { \mu ^2 } } \right] } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { y^2 } - \left( { 2\mu  + 2\sigma { '^2 } } \right)y + { { \left( { \mu  + \sigma { '^2 } } \right) }^2 } - { { \left( { \mu  + \sigma { '^2 } } \right) }^2 } + { \mu ^2 } } \right] } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { y^2 } - \left( { 2\mu  + 2\sigma { '^2 } } \right)y + { { \left( { \mu  + \sigma { '^2 } } \right) }^2 } - 2\mu \sigma { '^2 } - \sigma { '^4 } } \right] } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { { \left( { y - \left( { \mu  + \sigma { '^2 } } \right) } \right) }^2 } - 2\mu \sigma { '^2 } - \sigma { '^4 } } \right] } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }{ { \left[ { y - \left( { \mu  + \sigma { '^2 } } \right) } \right] }^2 } } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left( {  - 2\mu \sigma { '^2 } - \sigma { '^4 } } \right) } }dy } \\
 &= { e^{  - rt } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }{ { \left[ { y - \left( { \mu  + \sigma { '^2 } } \right) } \right] }^2 } } }{ e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }dy } \\
 &= { e^{  - rt } }{ e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left[ { y - \left( { \mu  + \sigma { '^2 } } \right) } \right] }^2 } } }{ { 2\sigma { '^2 } } } } }dy } \\
 &= { e^{ \left( { -rt + \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }\left[ { 1 - N\left( { \frac{ { \log K - \mu  - \sigma { '^2 } } }{ { \sigma ' } } } \right) } \right]\\
 &= { e^{ \left( { -rt + \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }N\left( \frac{ -\log K + \mu + \sigma { '^2 } }{ \sigma' } \right)\\
 &= { e^{ - rt + log{ S_0 } + \left( { r - \frac{ { { \sigma ^2 } } }{ 2 } } \right)t + \frac{ { { \sigma ^2 }t } }{ 2 } } }N\left[ { \frac{ 1 }{ { \sigma \sqrt t  } }\left( {  - \log K + log{ S_0 } + \left( { r - \frac{ { { \sigma ^2 } } }{ 2 } } \right)t + { \sigma ^2 }t } \right) } \right]\\
 &= { S_0 }{ e^{ - rt + rt - \frac{ { { \sigma ^2 }t } }{ 2 } + \frac{ { { \sigma ^2 }t } }{ 2 } } }N\left[ { \frac{ 1 }{ { \sigma \sqrt t  } }\left( { \log\frac{ { { S_0 } } }{ K } + \left( { r + \frac{ { { \sigma ^2 } } }{ 2 } } \right)t } \right) } \right]\\
 &= { S_0 }N\left[ { \frac{ 1 }{ { \sigma \sqrt t  } }\left( { \log\frac{ { { S_0 } } }{ K } + \left( { r + \frac{ { { \sigma ^2 } } }{ 2 } } \right)t } \right) } \right]
\end{align}$$


The second term:

$$\begin{align}
 - K{ e^{  - rt } }\int\limits_K^{  + \infty  } { { f_S }\left( S \right)dS } 
 &=  - K{ e^{  - rt } }\left[ { 1 - { F_S }\left( K \right) } \right] \\
 &=  - K{ e^{  - rt } }\left[ { 1 - N\left[ { \frac{ 1 }{ { \sigma \sqrt t  } } }\left( { \log K - \log{ S_0 } - \left( { r - \frac{ { { \sigma ^2 } } }{ 2 } } \right)t } \right) \right] } \right] \\
 &=  - K{ e^{  - rt } }\left[ { 1 - N\left[ { \frac{ 1 }{ { \sigma \sqrt t  } } }\left( { \log{ \frac{ K }{ S_0 } } - \left( { r - \frac{ { { \sigma ^2 } } }{ 2 } } \right)t } \right) \right] } \right] \\
 &=  - K{ e^{  - rt } }N\left[\frac{ 1 }{ { \sigma \sqrt t } }\left( { \log\frac{ S_0 }{ K } + \left( r - \frac{ \sigma ^2 }{ 2 } \right)t } \right) \right]
\end{align}$$

Combing the two terms, we have:

$$\begin{align}
\mathbb{ E^Q }\left[ { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  } } \right]
 &= { e^{  - rt } }\int\limits_K^{  + \infty  } { S{ f_S }\left( S \right)dS }  - K{ e^{  - rt } }\int\limits_K^{  + \infty  } { { f_S }\left( S \right)dS } \\
 &= { S_0 }N\left( d_1 \right) - K{ e^{  - rt } }N\left( d_2 \right)
\end{align}$$

where

$${d_1} = \frac{1}{ { \sigma \sqrt t } }\left[ { \log\frac{ S_0 }{ K } + \left( r + \frac{ \sigma ^2 }{ 2 } \right)t } \right]$$

$${d_2} = \frac{1}{ { \sigma \sqrt t } }\left[ { \log\frac{ S_0 }{ K } + \left( r - \frac{ \sigma ^2 }{ 2 } \right)t } \right]$$
