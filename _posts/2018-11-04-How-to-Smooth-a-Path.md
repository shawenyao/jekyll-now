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

In some cases, the *spline* method would have solved the problem already. However, it is not inconceivable to have a path so twisted that no function (in the mathematical sense) would be adequate to characterize all its trajectories, and this is where an alternative approach is needed.

## Problem Formulation
Given path $ABC$, find the optimal point $P$ such that path $APBC$ is visually smooth.
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_problem_formulation.svg" />
</p>

## A Heuristic Solution
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_heuristic_solution.svg" />
</p>

$$\overrightarrow{ P } = \overrightarrow{ D } + \lambda \| \overrightarrow{ AB } \| \left( 1 + \frac{ \overrightarrow{ BA } \cdot \overrightarrow{ BC } }{ \| \overrightarrow{ BA } \| \| \overrightarrow{ BC } \| } \right) \frac{ \overrightarrow{ CE } }{ \| \overrightarrow{ CE } \| }$$

where point $D$ is the midpoint between point $A$ and point $B$:

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
* how big $$\| \overrightarrow{ AB } \|$$ is

## Extension
What if we want more than one point between point $A$ and $B$? Naturally, after solving for point $P$, it can be viewed as part of the given path, so any level of interpolation can be achieved iteratively.

What about the last segment $BC$ where there is no more point ahead? The simplest answer would be to start all over again for the reversed path $CBA$. In fact, applying the algorithm twice (once **forward** and once **backward**) has at least one interesting implication: by taking the **average** between the two sets of interpolated points, we are further taking into account the curvature defined by the points behind as well as those ahead. This is arguably superior to interpolation along either direction alone.

## Putting It All Together
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_example.svg" />
</p>
