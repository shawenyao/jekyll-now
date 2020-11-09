---
layout: post
title: The Birth of a Galaxy
tag:
  - visualization
  - r
comments: true
draft: true
keyboard: true
new: true
---

Twinkle twinkle little star.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_0_demo.jpg" />
</div>
_Image by [NASA/JPL-Caltech/R. Hurt](https://solarsystem.nasa.gov/resources/285/the-milky-way-galaxy/)_

A few years ago, I [posted](/Milky-Way/) about creating a procedurally generated Milky Way. Note that the goal here aesthetic appeal rather than scientific accuracy.

## Problem Formulation

## Spiral Arms

[Archimedean spiral](https://en.wikipedia.org/wiki/Archimedean_spiral) makes really basis for the skeletons of the spiral arms . In polar coordinates,

$$
r = \theta ^ k
$$

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_1_spiral_arms_skeleton.jpg" />
</div>

## Let It Shine

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_2_star_unit.jpg" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_3_spiral_arms.jpg" />
</div>

## Galactic Center

$$
\begin{cases}
x = a \\ 
y = \rho a + \sqrt{1 - \rho ^ 2} b \\
\end{cases}
$$

Again, let's pick the color palette that best matches that of a burning core.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_4_galactic_center_unit.jpg" />
</div>



<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_5_galactic_center.jpg" />
</div>

## Putting It All Together

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/milky_way_large.jpg" />
</div>

I highly recommend viewing the image in its [native](https://shawenyao.github.io/R/output/milky_way/milky_way_large.jpg) resolution. You can also find [animation](https://shawenyao.github.io/R/output/milky_way/animation.html), [video](https://shawenyao.github.io/R/output/milky_way/video.html), [source](https://github.com/shawenyao/R/blob/master/main/milky_way/milky_way_plot_large.R), [Part II](/Milky-Way-Meets-Harmonograph/), or [merchandise](https://displate.com/displate/712287?art=5be7f871363ea).
