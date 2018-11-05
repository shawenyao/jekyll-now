---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation even when *spline* fails.

<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot1.svg" />
</p>

In some cases, the *spline* function would have solved the problem already. However, it is not inconceivable to have a path so twisted that a function (in the mathematical sense) would not be adequate to characterize all its the trajectories, and this is where an alternative approach is needed.

## Problem Formulation
Given a path $ABC$, find the optimal point $P$ such that path $APBC$ is visually smooth.
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_problem_formulation.svg" />
</p>

## A Heuristic Solution
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_heuristic_solution.svg" />
</p>



$$\overrightarrow{ P } = \overrightarrow{ D } + \lambda \| \overrightarrow{ AB } \| \left( 1 + \frac{ \overrightarrow{ BA } \cdot \overrightarrow{ BC } }{ \| \overrightarrow{ BA } \| \| \overrightarrow{ BC } \| } \right) \frac{ \overrightarrow{ CE } }{ \| \overrightarrow{ CE } \| }$$

where point $D$ is the middle point of point $A$ and point $B$:

$$\overrightarrow{ D } = \frac{ 1 }{ 2 } (\overrightarrow{ A } + \overrightarrow{ B })$$

and point $E$ is the projection of point $C$ on line $AB$:

$$\begin{cases}
\overrightarrow{ CE } \cdot \overrightarrow{ AB } = 0\\ 
\overrightarrow{ AE } = k \overrightarrow{BE}
\end{cases}$$

($k$ is a constant)

## Discussion
Intuitively, the position of point $P$ is a function of several factors:
* how big $\lambda$ is
* how big $\angle{ABC}$ is
* how long $\overrightarrow{ AB }$ is

## Extension
What if we want do the same for segment $BC$? The simplest way would be to start all over again for the reversed path $CBA$. In fact, applying the algorithm twice (once forward and once backward) has at least one interesting concequence: by taking the average between the two sets of interpolated points, we are essentilly taking into account the curvature defined by the points ahead as well as those behind. This is arguably superior to running the algorithm in either direction alone.

## Putting It All Together
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_example.svg" />
</p>
