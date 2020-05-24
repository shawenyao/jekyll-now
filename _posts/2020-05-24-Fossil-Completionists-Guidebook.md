---
layout: post
title: Fossil Completionist's Guidebook
tag:
  - maths
  - animal crossing
comments: true
draft: true
---

An estimate of how soon one can expect to complete the collection.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/006.jpg" />
</div>

There are 73 unique fossils in total to add to Blather's exhibition.

## Problem Formulation

Assuming equal chance of digging any fossil and 4 chances per day, how many days on average does it take to complete the collection?

## Numerical Solution

Simulations indicates that on average, it takes 89 days (or 356 trials) to collect all 73 types of fossils.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_1.png" />
</div>

On the other hand, if we look at the probability distribution at the end of the 89th day, there's a 58% chance that you will have completed the collection already.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_2.png" />
</div>

## Analytic Solution

Generally, if the probability of some random event happen is $x$, it takes $1 / x$ trials on average for it to occur at least once.

$$
\mathbb{E} \left[ T ^ N (n) \right] = \frac{ N }{ N+1-1 } + \frac{ N }{ N+1-2 } + \ ... \ +\frac{ N }{ N+1-(n-1) } +\frac{ N }{ N+1-n } 
$$

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_3.png" />
</div>

$$
\mathbb{E} \left[ F ^ N (t) \right] = 
\left\{ 
\begin{array}{c}
1, \ t = 1 \\ 
\mathbb{E} \left[ F ^ N (t - 1) \right] + \frac{ N - \mathbb{E} \left[ F ^ N (t - 1) \right] }{ N } , \ t > 1 \\ 
\end{array}
\right. 
$$

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_4.png" />
</div>

## Conclusions

The game was launched on March 20, 2020, so assuming you started playing on day 1 and never missed a single fossil, June 17th will be your benchmark to beat. Tip: remember to blame it on Zipper should you fail.

<br>

_This is Part III of my Animal Crossing post series. For Part II, see [here](/Modern-Portfolio-Theory-a-Case-Study-on-Turnips/)_.
