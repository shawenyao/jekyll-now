---
layout: post
title: Black-Scholes-Merton Formula
---

A step-by-step derivation.

$$ S = { S_0 }{ e^{ \left( { r - \frac{ { { \sigma^2 } } }{ 2 }} \right) t + \sigma \sqrt t x}} $$

$$ \log S = log{ S_0 } + \left( { r - \frac{ { { \sigma^2} } }{ 2 } } \right)t + \sigma \sqrt t x $$

$$ \mu  = log{ S_0 } + \left( {r - \frac{ { { \sigma ^2} } }{ 2 } } \right) t $$

$$ \sigma' = \sigma \sqrt t $$

$$ { f_S } \left( S \right) = \frac{ 1 }{ { S\sigma' \sqrt { 2\pi } } }{ e^{ - \frac{ { { { \left( { \log S - \mu } \right) }^2} } }{ { 2 { \sigma' } ^2 } } } } $$

$$ { F_S }\left( S \right) = N \left( { \frac{ { \log S - \mu } }{ { \sigma' } } } \right) $$



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
 &= { e^{ \left( { \mu  + \frac{ 1 }{ 2 }\sigma { '^2 } } \right) } }\left( -log K + \mu + \sigma { '^2 } \right)\\
\end{align}$$

