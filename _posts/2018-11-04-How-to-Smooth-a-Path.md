---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
comments: true
dog: true
---

Context-aware interpolation even when *spline* fails.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/smooth_path/plot1.svg" />
</div>

One of the issues I ran into when writing about [Map of BART](/Map-of-BART/) was, literally connecting the dots wasn't able to produce paths as aesthetically pleasing as I had hoped for. They are a bit too edgy for my taste, especially where the lines connect.

In some cases, the [*spline interpolation*](https://en.wikipedia.org/wiki/Spline_interpolation) method could come in handy. However, it is not inconceivable to have a path so twisted that no function (in the mathematical sense) would be adequate to characterize the trajectories entirely, and this is where an alternative approach is called for.

## Problem Formulation
Given path $ABC$, find the optimal point $P$ such that path $APBC$ is visually smooth.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/smooth_path/plot_problem_formulation.svg" />
</div>

## A Heuristic Solution
<div align="center">
  <img src="https://shawenyao.github.io/R/output/smooth_path/plot_heuristic_solution.svg" />
</div>

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
What if we want more than one point between point $A$ and $B$? After solving for point $P$, it naturally becomes part of the given path, so any level of interpolation can be achieved **iteratively**.

What about the last segment $BC$ where there's no more point ahead? The simplest answer would be to start all over again for the reversed path $CBA$. In fact, applying the algorithm twice (once **forward** and once **backward**) has at least one practical implication: by taking the **average** between the two sets of interpolated points, we are further taking into account the curvature defined by the points behind as well as those ahead. This is arguably superior to interpolation along either direction alone.

## Putting It All Together
<div align="center">
  <img src="https://shawenyao.github.io/R/output/smooth_path/plot_example.svg" />
</div>

As the name indicates, there isn't much the forward/backward-looking approach can do when it comes to the last/first segment of the path, and this is where the average method shines the brightest.

## Final Thoughts: the Effect of $\lambda$
$\lambda$ determines how sensitive the position of the interpolated point $P$ is to the change in $\angle{ABC}$ and $$\| \overrightarrow{ AB } \|$$, so how does the choice of $\lambda$ affect the outcome? A small $\lambda$ probably won't be very useful as it is going to produce something too similar to the original path. Meanwhile, a large $\lambda$ will break the interpolation in a different way by overstating the curvature. Somewhere in between lies the sweet spot, which turns out to be $0.25$ in my case.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/smooth_path/plot_lambda.svg" />
</div>
