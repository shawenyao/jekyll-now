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

A few years ago, I [posted](/Milky-Way/) an image of procedurally generated Milky Way without explaining how. Note that the goal here aesthetic appeal rather than scientific accuracy.

## Problem Formulation

I

## Spiral Arms

[Archimedean spiral](https://en.wikipedia.org/wiki/Archimedean_spiral) makes a really nice basis for the skeletons of the spiral arms . In polar coordinates,

$$
r = \theta ^ k
$$

$$
\begin{cases}
x = \theta ^ k \cos{\theta} \\ 
y = \theta ^ k \sin{\theta} \\
\end{cases}
$$

```r
tibble(
  theta = seq(from = theta_from, to = theta_to, length.out = theta_length)
) %>% 
  mutate(
    r = theta ^ k,
    x = r * cos(theta),
    y = r * sin(theta)
  )
```

What if we want more than 1 spiral arm? Simply repeat the above N times and each time, add a constant to theta in order to rotate the polar coordinates:

```r
num_of_arms <- 4
lapply(
  list(id = seq_len(num_of_arms)),
  function(id, theta_from, theta_to, arm_width){
    tibble(
      id = id,
      theta = seq(from = theta_from, to = theta_to, length.out = theta_length)
    ) %>% 
      mutate(
        r = theta ^ theta_power,
        x = r * cos(theta + 2 * pi * id / num_of_arms),
        y = r * sin(theta + 2 * pi * id / num_of_arms)
      )
  }) %>% 
  bind_rows()
```

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

Again, let's pick the color palette best matching that of a burning core.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_4_galactic_center_unit.jpg" />
</div>



<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_5_galactic_center.jpg" />
</div>

## Putting It All Together

From someone who lacks training in cosmology in any meaningful way, the end product works surprisingly well. Randomness is truly our friend in creating the illusion of controlled predictability, and our choice of colors/transparency/shape/size all after various trials and errors.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/milky_way_large.jpg" />
</div>

I highly recommend viewing the image in its [native](https://shawenyao.github.io/R/output/milky_way/milky_way_large.jpg) resolution. You can also find [animation](https://shawenyao.github.io/R/output/milky_way/animation.html), [video](https://shawenyao.github.io/R/output/milky_way/video.html), [source](https://github.com/shawenyao/R/blob/master/main/milky_way/milky_way_plot_large.R), [Part II](/Milky-Way-Meets-Harmonograph/), or [merchandise](https://displate.com/displate/712287?art=5be7f871363ea).
