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

Universe by tidyverse.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_0_demo.jpg" />
</div>
_Image by [NASA/JPL-Caltech/R. Hurt](https://solarsystem.nasa.gov/resources/285/the-milky-way-galaxy/)_

A few years ago, I [posted](/Milky-Way/) an image of procedurally generated Milky Way without explaining how. Note that the goal here aesthetic appeal rather than scientific accuracy.

## Problem Formulation

I

## Spiral Arms

At first glance, [Archimedean spiral](https://en.wikipedia.org/wiki/Archimedean_spiral) bears remarkable resemblance to the spiral arms. In polar coordinates, the curve is given by:

$$
r = \theta ^ k
$$

Equivalently, the Cartesian coordinates would be:

$$
\begin{cases}
x = \theta ^ k \cos{\theta} \\ 
y = \theta ^ k \sin{\theta} \\
\end{cases}
$$

In the language of tidyverse, once we have the desired range of $\theta$, the full set of points can be created by:

```r
spiral_arm <- tibble(
  theta = seq(from = theta_from, to = theta_to, length.out = theta_length)
) %>% 
  mutate(
    r = theta ^ k,
    x = r * cos(theta),
    y = r * sin(theta)
  )
```

Now, what if we want more than one spiral arm? One idea would be to repeat the process above and add a constant to theta for rotation purposes:

```r
spiral_arms <- lapply(
  list(id = seq_len(num_of_arms)),
  function(id, theta_from, theta_to, arm_width){
    tibble(
      id = id,
      theta = seq(from = theta_from, to = theta_to, length.out = theta_length)
    ) %>% 
      mutate(
        r = theta ^ k,
        x = r * cos(theta + 2 * pi * id / num_of_arms),
        y = r * sin(theta + 2 * pi * id / num_of_arms)
      )
  }) %>% 
  bind_rows()
```

That gives us the skeleton upon which the galaxy is going to be built.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_1_spiral_arms_skeleton.jpg" />
</div>

## Fleshing out the Skeleton

Stars rarely align exactly on a line. Instead, they exhibit some degree of duality between individual randomness and collective predictability. We can jitter the points vertically and horizontally to achieve similar effects. If there aren't enough points, reuse the same data frame!

```r
stars <- sprial_arms %>% 
  slice(rep(row_number(), star_intensity)) %>% 
  mutate(
    x = x + rnorm(n(), sd = width),
    y = y + rnorm(n(), sd = width)
  )
```

There are two moving parts here. First, the intensity variable controls overall how many stars will be created. On the other hand, the standard deviation of the noise governs the dispersion of how far a star tends to diverge from its spiral arm. Also note that according R's plotting convention, shape number 8 gives us the star-shaped point we want.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_3.0_spiral_arms.jpg" />
</div>

There seems to be one problem - why don't the stars shine?

## Twinkle Twinkle Little Star

Obviously, black isn't the greatest choice of color when it comes to stars. It's a subjective call but personally I prefer these:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_2_star_unit.jpg" />
</div>

Next, colors can be attached to the stars by randomly sampling from the color space with replacement.

```r
stars <- stars %>%
  mutate(
    color = star_colors %>% sample(size = n(), replace = TRUE)
  )
```

In fact, we can do the randomize other attributes of the stars as well, i.e., either by sampling values from a predefined set (e.g., random sizes of the stars) or letting it correlate with some feature (e.g., transparency should be proportional to the radius from the center). Adding multiple layers of halo effect also helps with introducing the illusion of a vibrant galaxy.

```r
ggplot(sprial_arms, aes(x = x, y = y)) +
  geom_point(data = stars, size = star_halo_size1, color = "white", shape = 8) +
  geom_point(data = stars, size = star_halo_size2, color = "white", shape = 8) +
  geom_point(data = stars, size = stars$size, alpha = stars$alpha, color = stars$color, shape = 8) +
  theme(panel.background = element_rect(fill = background_color))
```

Lo and behold. When all is being thrown onto a dark canvas, we've got ourselves a galaxy.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_3_spiral_arms.jpg" />
</div>

Before we move on, let's take a momment to appreciate how far we've come since drawing the skeleton. However, something is missing.

## Galactic Center

At the heart of the Milky Way lies the brightest region of our galaxy, the [Galactic Center](https://en.wikipedia.org/wiki/Galactic_Center). From a purely visual standpoint, it looks like a tilted oval spanning from bottom left to top right.

Voila - this isn't hard to find in geometry. Recall multivariate normal distribution?

$$
\begin{cases}
x = a \\ 
y = \rho a + \sqrt{1 - \rho ^ 2} b \\
\end{cases}
$$

where $a$ and $b$ are independent normally distributed random variables. This should give us a way to generate data points similar in shape to the Galactic Center:

```r
gc <- tibble(
    x = rnorm(gc_intensity, sd = gc_sd_x)
) %>% 
  mutate(
    y = gc_rho * x + sqrt(1 - gc_rho ^ 2) * rnorm(n(), sd = gc_sd_y)
  )
```

Again, let's pick the color palette best matching that of a burning furnace:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_4_galactic_center_unit.jpg" />
</div>

As usual, we pull the trick of color, size, transparency as well as halo effect:

```r
ggplot(sprial_arms, aes(x = x, y = y)) +
  geom_point(data = gc, size = gc_halo_size1, alpha = gc_halo_alpha1, color = "gold", shape = 8) +
  geom_point(data = gc, size = gc_halo_size2, alpha = gc_halo_alpha2, color = "gold", shape = 8) +
  geom_point(data = gc, size = gc$size, alpha = gc$alpha, color = gc$color, shape = 8) +
  theme(panel.background = element_rect(fill = background_color))
```

Between you and me, who would have thought that something as massive as the Galactic Center is actually two Gaussian variables in disguise?

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/plot_5_galactic_center.jpg" />
</div>

## Putting It All Together

From someone who lacks training in cosmology in any meaningful way, the end product works surprisingly well. In all fairness, most of the credit goes to our friend randomness who manages to create a sense of guided unpredictability. Moreover, our choices of color palette, transparency, shape and size all seem to have come together in harmony after various trials and errors.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/milky_way/milky_way_large.jpg" />
</div>

I highly recommend viewing the image in its [native](https://shawenyao.github.io/R/output/milky_way/milky_way_large.jpg) resolution. You can also find [animation](https://shawenyao.github.io/R/output/milky_way/animation.html), [video](https://shawenyao.github.io/R/output/milky_way/video.html), [source](https://github.com/shawenyao/R/blob/master/main/milky_way/milky_way_plot_large.R), [part two](/Milky-Way-Meets-Harmonograph/), or [merchandise](https://displate.com/displate/712287?art=5be7f871363ea).
