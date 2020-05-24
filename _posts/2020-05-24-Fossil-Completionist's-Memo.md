---
layout: post
title: Fossil Completionist's Memo
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

$$
\begin{align}
F_Q(x) 
&= \mathbb{P}(Q \leq x) \\
&= \mathbb{P}(max(P_1, P_2, ..., P_N) \leq x) \\
&= \mathbb{P}(P_1 \leq x \ ∩ \ P_2 \leq x \ ∩ \ ... \ ∩ \ P_N \leq x) \\
&= \mathbb{P}(P_1 \leq x) \mathbb{P}(P_2 \leq x) \ ... \ \mathbb{P}(P_N \leq x) \\
&= G^{N}(x) \\
\end{align}
$$


<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_1.png" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_2.png" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_3.png" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/fossils_collector_4.png" />
</div>

<br>

_This is Part III of my Animal Crossing post series. For Part II, see [here](/Modern-Portfolio-Theory-a-Case-Study-on-Turnips/)_.
