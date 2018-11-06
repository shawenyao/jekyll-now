---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation even when *spline* fails.

One of the issues I initially ran into when creating [Map of BART](/Map-of-BART/) was, literally connecting the dots wasn't able to produce paths as aesthetically pleasing as I had hoped for. They are a bit too edgy for my taste, especially around the connection points.

<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot1.svg" />
</p>

In some cases, the [*spline interpolation*](https://en.wikipedia.org/wiki/Spline_interpolation) method would come in handy. However, it is not inconceivable to have a path so twisted that no function (in the mathematical sense) would be adequate to characterize the trajectories in its entirety, and this is where an alternative approach is needed.

## Problem Formulation
Given path $ABC$, find the optimal point $P$ such that path $APBC$ is visually smoother.
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_problem_formulation.svg" />
</p>

## A Heuristic Solution
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_heuristic_solution.svg" />
</p>

$$\overrightarrow{ P } = \overrightarrow{ D } + \lambda \| \overrightarrow{ AB } \| \left( 1 + \cos \angle{ABC} \right) \frac{ \overrightarrow{ CE } }{ \| \overrightarrow{ CE } \| }$$

where $\cos \angle{ABC}$ is given by:

$$\cos \angle{ABC} = \frac{ \overrightarrow{ BA } \cdot \overrightarrow{ BC } }{ \| \overrightarrow{ BA } \| \| \overrightarrow{ BC } \| }$$

point $D$ is the midpoint between point $A$ and point $B$:

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
What if we want more than one point between point $A$ and $B$? Naturally, after solving for point $P$, it can be viewed as part of the given path, so any level of interpolation can be achieved **iteratively**.

What about the last segment $BC$ where there's no more point ahead? The simplest answer would be to start all over again for the reversed path $CBA$. In fact, applying the algorithm twice (once **forward** and once **backward**) has at least one interesting implication: by taking the **average** between the two sets of interpolated points, we are further taking into account the curvature defined by the points behind as well as those ahead. This is arguably superior to interpolation along either direction alone.

## Putting It All Together
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_example.svg" />
</p>
