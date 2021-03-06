---
layout: post
title: When Will N(d1) Become the Probability of Exercising an Option?
tag:
  - maths
  - finance
comments: true
maths: true
---

A proof by comparing change of measure with the Black-Scholes formula.

Consider the value of a vanilla European call option:

$$\begin{align}
Call(0) &= \mathbb{ E^Q } \left[ \frac{ { \left [ S(T)-K \right ] }^{ + } }{ B(T) } \right] \\
 &=\mathbb{ E^Q } \left[ \frac{ { \left [ S(T)-K \right ] } { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] \\
 &={ \mathbb{ E^Q } \left[ \frac{ { S(T) } { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] } - { \mathbb{ E^Q } \left[ \frac{ {  K  } { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] } \\
 &={ \mathbb{ E^Q } \left[ \frac{ { S(T) } { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] } - { K \ \mathbb{ E^Q } \left[ \frac{ { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] } \\
 &={ \mathbb{ E^Q } \left[ \frac{ { S(T) } { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] B(0) } - { K \ \mathbb{ E^Q } \left[ \frac{ { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] B(0) } \\
 &={ \mathbb{ E^S } \left[ \frac{ { S(T) } { \textbf{ 1 } _ { S(T)>K } } }{ S(T) } \right] S(0) } - { K \ \mathbb{ E^{ Q^T } } \left[ \frac{ { \textbf{ 1 } _ { S(T)>K } } }{ P(T,T) } \right] P(0,T) } \\
 &={ \mathbb{ E^S } \left[ { \textbf{ 1 } _ { S(T)>K } } \right] S(0) } - { K \ \mathbb{ E^{ Q^T } } \left[ { \textbf{ 1 } _ { S(T)>K } } \right] P(0,T) } \\
 &={ \mathbb{ P^S } \left[ S(T)>K \right] S(0) } - { K \ \mathbb{ P^{ Q^T } } \left[ S(T)>K \right] P(0,T) } \\
 &={ \mathbb{ P^S } \left[ S(T)>K \right] S(0) } - { \mathbb{ P^{ Q^T} } \left[ S(T)>K \right] K P(0,T) }
\end{align}$$

Assuming constant interest rate:

$$ P(0,T)=e^{ -rT } $$

we have:

$$ Call(0)={ \mathbb{ P^S } \left[ S(T)>K \right] S(0) } - { \mathbb{ P^{ Q^T } } \left[ S(T)>K \right] K e^{ -rT } } $$

Compare this with the Black-Scholes formula:

$$ Call(0)={ N(d_1)S(0) }-{ N(d_2)K e^{ -rT } } $$

Since both formulas hold true for any choice of the parameters, we have:

$$ N(d_1)=\mathbb{ P^S } \left[ S(T)>K \right] $$

$$ N(d_2)=\mathbb{ P^ { Q^T } } \left[ S(T)>K \right] $$

In other words, $N(d_1)$ is the probability of exercising the option under the stock measure, while $N(d_2)$ is the probability of exercising the option under the T-forward measure (and of course, the risk-neutral measure as well).
