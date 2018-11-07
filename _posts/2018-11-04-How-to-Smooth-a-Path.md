---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation even when *spline* fails.

One of the issues I ran into when writing about [Map of BART](/Map-of-BART/) was, literally connecting the dots wasn't able to produce paths as aesthetically pleasing as I had hoped for. They are a bit too edgy for my taste, especially where the lines connect.

<p align="center">
  <img src="https://shawenyao.github.io/R/output/smooth_path/plot1.svg" />
</p>

In some cases, the [*spline interpolation*](https://en.wikipedia.org/wiki/Spline_interpolation) method could come in handy. However, it is not inconceivable to have a path so twisted that no function (in the mathematical sense) would be adequate to characterize the trajectories in its entirety, and this is where an alternative approach is called for.


