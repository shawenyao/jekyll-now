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

## Problem Formulation

## Solution

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_1.png" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_2.png" />
</div>

## Analytic Solution

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
1 + (1 - \frac{ 1 }{ N }) \mathbb{E} \left[ F ^ N (t - 1) \right] , \ t > 1 \\ 
\end{array}
\right. 
$$

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_4.png" />
</div>

<br>

_This is Part III of my Animal Crossing post series. For Part II, see [here](/Modern-Portfolio-Theory-a-Case-Study-on-Turnips/)_.
