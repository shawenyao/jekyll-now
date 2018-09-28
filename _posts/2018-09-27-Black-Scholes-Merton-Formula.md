---
layout: post
title: Black-Scholes-Merton Formula
---

A step-by-step derivation.

$$ S = { S_0 }{ e^{ \left( { r - \frac{ { { \sigma^2 } } }{ 2 }} \right) t + \sigma \sqrt t x}} $$

$$ \log S = log{ S_0 } + \left( { r - \frac{ { { \sigma^2} } }{ 2 } } \right)t + \sigma \sqrt t x $$

$$ \mu  = log{ S_0 } + \left( {r - \frac{ { { \sigma ^2} } }{ 2 } } \right) t $$

$$ \sigma' = \sigma \sqrt t $$

$$ { p_S } \left( S \right) = \frac{ 1 }{ { S\sigma' \sqrt { 2\pi } } }{ e^{ - \frac{ { { { \left( { \log S - \mu } \right) }^2} } }{ { 2 { \sigma' } ^2 } } } } $$

$$ { N_S }\left( S \right) = N \left( { \frac{ { \log S - \mu } }{ { \sigma' } } } \right) $$

Consider the value of a vanilla European call option:

$$\begin{align}
\mathbb{ E }\left[ { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  } } \right]
 &= \int\limits_{  - \infty  }^{  + \infty  } { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  }{ p_S }\left( S \right)dS } \\
 &= \int\limits_{  - \infty  }^K { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  }{ p_S }\left( S \right)dS }  + \int\limits_K^{  + \infty  } { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  }{ p_S }\left( S \right)dS } \\
 &= \int\limits_K^{  + \infty  } { { e^{  - rt } }\left( { S - K } \right){ p_S }\left( S \right)dS } \\
 &= \int\limits_K^{  + \infty  } { { e^{  - rt } }S{ p_S }\left( S \right)dS }  - \int\limits_K^{  + \infty  } { { e^{  - rt } }K{ p_S }\left( S \right)dS } \\
 &= { e^{  - rt } }\int\limits_K^{  + \infty  } { S{ p_S }\left( S \right)dS }  - K{ e^{  - rt } }\int\limits_K^{  + \infty  } { { p_S }\left( S \right)dS } 
\end{align}$$

The first term:

$$\begin{align}
{ e^{  - rt  }  }\int\limits_K^{  + \infty   } { S{ p_S  }\left( S \right)dS  }
 &= { e^{  - rt  }  }{ e^{ \mu  + { { \sigma { '^2  }  } \mathord{ \left/
 { \vphantom { { \sigma { '^2  }  } 2  }  } \right.
 \kern-\nulldelimiterspace  } 2  }  }  }N\left( { \frac{ {  - \log K + \mu  + \sigma { '^2  }  }  }{ { \sigma '  }  }  } \right)\\
 &= { e^{  - rt  }  }{ e^{ log{ S_0  } + \left( { r - \frac{ { { \sigma ^2  }  }  }{ 2  }  } \right)t + \frac{ { { \sigma ^2  }t  }  }{ 2  }  }  }N\left( { \frac{ 1  }{ { \sigma \sqrt t   }  }\left( {  - \log K + log{ S_0  } + \left( { r - { { { \sigma ^2  }  } \mathord{ \left/
 { \vphantom { { { \sigma ^2  }  } 2  }  } \right.
 \kern-\nulldelimiterspace  } 2  }  } \right)t + { \sigma ^2  }t  } \right)  } \right)\\
 &= { S_0  }{ e^{  - rt + rt - { { { \sigma ^2  }  } \mathord{ \left/
 { \vphantom { { { \sigma ^2  }  } 2  }  } \right.
 \kern-\nulldelimiterspace  } 2  } + { { { \sigma ^2  }t  } \mathord{ \left/
 { \vphantom { { { \sigma ^2  }t  } 2  }  } \right.
 \kern-\nulldelimiterspace  } 2  }  }  }N\left( { \frac{ 1  }{ { \sigma \sqrt t   }  }\left( { log\frac{ { { S_0  }  }  }{ K  } + \left( { r + { { { \sigma ^2  }  } \mathord{ \left/
 { \vphantom { { { \sigma ^2  }  } 2  }  } \right.
 \kern-\nulldelimiterspace  } 2  }  } \right)t  } \right)  } \right)\\
 &= { S_0  }N\left( { { d_ +   }  } \right)
\end{align}$$

$$\begin{align}
\int\limits_K^{  + \infty  } { S{ p_S }\left( S \right)dS }
 &= \int\limits_K^{  + \infty  } { S\frac{ 1 }{ { S\sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { \log S - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }dS } \\
 &= \int\limits_K^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { \log S - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }dS } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { y - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }d\left( { { e^y } } \right) } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ { { e^y } } }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { y - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left( { y - \mu  } \right) }^2 } } }{ { 2\sigma { '^2 } } } + y } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left( { { y^2 } - 2y\mu  + { \mu ^2 } - 2\sigma { '^2 }y } \right) } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { y^2 } - \left( { 2\mu  + 2\sigma { '^2 } } \right)y + { \mu ^2 } } \right] } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { y^2 } - \left( { 2\mu  + 2\sigma { '^2 } } \right)y + { { \left( { \mu  + \sigma { '^2 } } \right) }^2 } - { { \left( { \mu  + \sigma { '^2 } } \right) }^2 } + { \mu ^2 } } \right] } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { y^2 } - \left( { 2\mu  + 2\sigma { '^2 } } \right)y + { { \left( { \mu  + \sigma { '^2 } } \right) }^2 } - 2\mu \sigma { '^2 } - \sigma { '^4 } } \right] } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left[ { { { \left( { y - \left( { \mu  + \sigma { '^2 } } \right) } \right) }^2 } - 2\mu \sigma { '^2 } - \sigma { '^4 } } \right] } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }{ { \left[ { y - \left( { \mu  + \sigma { '^2 } } \right) } \right] }^2 } } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }\left( {  - 2\mu \sigma { '^2 } - \sigma { '^4 } } \right) } }dy } \\
 &= \int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ 1 }{ { 2\sigma { '^2 } } }{ { \left[ { y - \left( { \mu  + \sigma { '^2 } } \right) } \right] }^2 } } }{ e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }dy } \\
 &= { e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }\int\limits_{ \log K }^{  + \infty  } { \frac{ 1 }{ { \sigma '\sqrt { 2\pi  }  } }{ e^{  - \frac{ { { { \left[ { y - \left( { \mu  + \sigma { '^2 } } \right) } \right] }^2 } } }{ { 2\sigma { '^2 } } } } }dy } \\
 &= { e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }\left[ { 1 - N\left( { \frac{ { \log K - \mu  - \sigma { '^2 } } }{ { \sigma ' } } } \right) } \right]\\
 &= { e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }N\left( \frac{ -\log K + \mu + \sigma { '^2 } }{ \sigma' } \right)\\
\end{align}$$


The second term:

$$\begin{align}
 - K{ e^{  - rt } }\int\limits_K^{  + \infty  } { { p_S }\left( S \right)dS }
 &=  - K{ e^{  - rt } }\left( { 1 - { F_S }\left( K \right) } \right)\\
 &=  - K{ e^{  - rt } }\left( { 1 - N\left( { \frac{ { \log K - log{ S_0 } - \left( { r - \frac{ { { \sigma ^2 } } }{ 2 } } \right)t } }{ { \sigma \sqrt t  } } } \right) } \right)\\
 &=  - K{ e^{  - rt } }\left( { 1 - N\left( { \frac{ {  - log\frac{ { { S_0 } } }{ K } - \left( { r - { { { \sigma ^2 } } \mathord{ \left/
 { \vphantom { { { \sigma ^2 } } 2 } } \right.
 \kern-\nulldelimiterspace } 2 } } \right)t } }{ { \sigma \sqrt t  } } } \right) } \right)\\
 &=  - K{ e^{  - rt } }\left( { 1 - N\left( {  - { d_ -  } } \right) } \right)\\
 &=  - K{ e^{  - rt } }N\left( { { d_ -  } } \right)
\end{align}$$

Combingh the two terms, we have:

$$\begin{align}
\mathbb{ E }\left[ { { e^{  - rt } }{ { \left( { S - K } \right) }^ +  } } \right]
 &= { e^{  - rt } }\int\limits_K^{  + \infty  } { S{ p_S }\left( S \right)dS }  - K{ e^{  - rt } }\int\limits_K^{  + \infty  } { { p_S }\left( S \right)dS } \\
 &= { S_0 }N\left( d_1 \right) - K{ e^{  - rt } }N\left( d_2 \right)
\end{align}$$

where

$$ N\left( d_1 \right) =  $$

$$ N\left( d_2 \right) = $$
