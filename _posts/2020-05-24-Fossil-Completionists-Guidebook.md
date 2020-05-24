---
layout: post
title: Fossil Completionist's Guidebook
tag:
  - animal crossing
  - maths
comments: true
draft: false
---

My attempt at relieving fossil collector's anxiety.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/006.jpg" />
</div>

In _Animal Crossing: New Horizons_, every starfish-shaped crack is another chance for glory because once you dig up a new fossil, you can then donate it to Blathers the museum curator. After an enthusiastic but rather unsolicited introduction about the fossil's origin story, it becomes a permanent part of the exhibition for you and your friends to enjoy.

If you are like me, all was well until the honeymoon phase started to wear out and at some point, you began to get nothing but duplicates. Days turned into weeks before you knew it yet things didn't get any better, and you are on the verge of suspecting foul play. Could Nintendo be deliberately withholding a few fossils from your reach just to keep you coming back? Could it be a marketing campaign to sell you the online membership where trading with friends is the only way to advance? Or could it be the case that you simply got unlucky again, as with everything else in life?

In this post, I study the problem of how long it takes on average to complete the fossil collection. As the answer suggests, it is still too early to be concerned and everyone has at least until June 17th to 1) doubt if the game is rigged and/or 2) be considered unlucky.

## General Setup

First things first, there are a few important facts to keep in mind before we get started:
* for tractability, it is assumed that each fossil has an equal chance of being dug up (comment below if you disagree!)
* 4 fossils can be found on any given day
* there are 73 unique fossils in total to add to the museum's collection

## Numerical Solution

With the help of any modern computing device, numerical simulation indicates that on average, it takes 89 days (or 356 trials) to collect all fossils. So there you go - it's not that bad.

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

where $N$ is the total number of unique collectibles. It grows almost linearly at first (as it's fairly unlikely to get duplicates already), but the last one is expected to cost you $N$ tries.

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

Again, initially it fills out almost linearly. The curve starts to flatten out eventually as you build up your collection, desperately waiting for the last few pieces to arrive. That said, all you really need is to keep calm and carry on - as previously mentioned, the odds are in your favor in 3 months' time (and increasingly so).

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_4.png" />
</div>

## Conclusions

_Animal Crossing: New Horizons_ was launched on March 20, 2020, so if you started playing on day 1 and never missed a single fossil, June 17th (i.e., day 89) will be your benchmark to beat. Should that not be the case, you can always blame it on Zipper!

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/007.jpg" />
</div>

<br>

_This is Part III of my Animal Crossing post series. For Part II, see [here](/Modern-Portfolio-Theory-a-Case-Study-on-Turnips/)_.
