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

Assuming equal chance of digging up any fossil and 4 chances per day, how many days on average does it take to complete the collection (i.e., 73 distinct entries)?

## Numerical Solution

Simulations indicates that on average, it takes 89 days (or 356 trials) to collect all 73 types of fossils.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_1.png" />
</div>

Furthermore, if we look at the probability distribution at the end of the 89th day, more likely than not you will have completed the collection already.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_2.png" />
</div>

## Analytic Solution

Generally, if the probability of some random event happening is $x$, it takes $1 / x$ trials on average for it to occur at least once. Adding all expected number of trials to collect the first $n$ fossils together, we have:

$$
\mathbb{E} \left[ T ^ N (n) \right] = \frac{ N }{ N+1-1 } + \frac{ N }{ N+1-2 } + \ ... \ +\frac{ N }{ N+1-(n-1) } +\frac{ N }{ N+1-n } 
$$

where $N$ is the number of total unique number of collectibles. It grows almost linearly at first (as it's fairly unlikely to get duplicates already), but the last one is expected to cost you $N$ tries.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_3.png" />
</div>

The expected number of unique fossils as a function of the number of trials tells the other side of the story. For each new trial, the incremental contribution to the collection in terms of additional "uniqueness" equals the probability of finding something that has not been found so far:

$$
\mathbb{E} \left[ F ^ N (t) \right] = 
\left\{ 
\begin{array}{c}
1, \ t = 1 \\ 
\mathbb{E} \left[ F ^ N (t - 1) \right] + \frac{ N - \mathbb{E} \left[ F ^ N (t - 1) \right] }{ N } , \ t \geq 2 \\ 
\end{array}
\right. 
$$

Again, initially it fills out almost linearly. The curve starts to flatten out as you build up your collection, anxiously waiting for the last few pieces to arrive.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_4.png" />
</div>

## Conclusions

_Animal Crossing: New Horizons_ was launched on March 20, 2020, so if you started playing on day 1 and never missed a single fossil, June 17th will be your benchmark to beat. Tip: remember to blame it on Zipper should you fail!

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/007.jpg" />
</div>

<br>

_This is Part III of my Animal Crossing post series. For Part II, see [here](/Modern-Portfolio-Theory-a-Case-Study-on-Turnips/)_.
