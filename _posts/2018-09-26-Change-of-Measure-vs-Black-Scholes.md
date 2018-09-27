---
layout: post
title: Change of Measure vs Black-Scholes
---

test

Consider the value of a call option:

$Call(0)$

$=E^Q \left[ \frac{ { \left [ S(T)-K \right ] }^{ + } }{ B(T) } \right]$

$=E^Q \left[ \frac{ { \left [ S(T)-K \right ] } { \textbf{ 1 }_{ S(T)>K } } }{ B(T) } \right]$

$={ E^Q \left[ \frac{ { S(T) } { \textbf{ 1 }_{ S(T)>K } } }{ B(T) } \right] } - { E^Q \left[ \frac{ {  K  } { \textbf{ 1 } _ { S(T)>K } } }{ B(T) } \right] }$

$={ E^Q \left[ \frac{ { S(T) } { \textbf{ 1 }_{ S(T)>K } } }{ B(T) } \right] } - { K E^Q\left[ \frac{ { \textbf{ 1 }_{ S(T)>K } } }{ B(T) } \right] }$

$={ E^Q \left[ \frac{ { S(T) } { \textbf{ 1 }_{ S(T)>K } } }{ B(T) } \right] B(0) } - { K E^Q\left[ \frac{ { \textbf{ 1 }_{ S(T)>K } } }{ B(T) } \right] B(0) }$

$={ E^S \left[ \frac{ { S(T) } { \textbf{ 1 }_{ S(T)>K } } }{ S(T) } \right] S(0) } - { K E^{ Q^T }\left[ \frac{ { \textbf{ 1 }_{ S(T)>K } } }{ P(T,T) } \right] P(0,T) }$

$={ E^S \left[ { \textbf{ 1 }_{ S(T)>K } } \right] S(0) } - { K E^{ Q^T }\left[ { \textbf{ 1 }_{ S(T)>K } } \right] P(0,T) }$

$=Q^S \left[ S(T)>K \right] S(0) - K Q^T \left[ S(T)>K \right] P(0,T)$

$=Q^S \left[ S(T)>K \right] S(0) - Q^T \left[ S(T)>K \right] K P(0,T)$

Compare with the Black-Scholes formula:

$Call(0)=N(d_1)S(0)-N(d_2)K e^{ -rT }$

and assuming constant interest rate:

$P(0,T)=e^{ -rT }$

then we have:

$N(d_1)=Q^S \left[ S(T)>K \right]$

$N(d_2)=Q^T \left[ S(T)>K \right]$

So $N(d_1)$ is the probability of exercising the option under the stock measure,

and $N(d_2)$ is the probability of exercising the option under the T-forward measure.
