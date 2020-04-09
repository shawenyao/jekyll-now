---
layout: post
title: Where is My Island
tag:
  - maths
  - animal crossing
comments: true
draft: true
---

Locating your _Nook Inc._ getaway package.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/001.jpg" />
</div>

I've been playing _Animal Crossing: New Horizons_, where my in-game character flew to a deserted island in order to start a new life. Despite its cartoony art style, the game manages to establish an astonishing level of realism, to the point where it almost feels like a living and breathing world. For example, I know for a fact that my island exists somewhere in the northern hemisphere; I know that the sun rises and sets there every real-world day; I know that the seasons rotate and spring is coming. At some point, I start wonder how much further I can push this, e.g., given what's observable in the game, can I deduce where my island is? If so, where is it?

In this post, please join me for a tour to my island, and I will unveil its location at the end (sort of).

## The Longitude
Due to the fact that the game runs on real-world clock, my deserted island must be conveniently located in the same time zone as where I physically am (or at least wherever my system is set). Voila! There it is and it can't be too far off.

## The Latitude
Figuring out the latitude can get a little tricky. In a nutshell, it boils down to measuring the _solar elevation angle_ at _solar noon_. Astronomy tells us that the following equation holds true:

$$
h = 90^\text{o} - \left| \phi - \delta \right|
$$

where
* $h$ is the solar elevation angle at solar noon. It is also the angle between a ray of sunlight and the horizon at the observation point. Also, solar noon is defined as the time of the day when the Sun reachest the highest point (note that this is equivalent to the length of shadow being the shortest).
* $\phi$ is the latitude of the observation point (a positive number in this case)
* $\delta$ is the latitude of the subsolar point (a negative number in this case), also know as the solar declination angle.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/solar_zenith_angle/1_label.png" />
</div>

For full reference, see [here](https://en.wikipedia.org/wiki/Solar_zenith_angle), [here](https://commons.wvc.edu/rdawes/ASTR217/Gnomon.pdf) and [here](https://vortex.plymouth.edu/sun/sun4a.html)

There's yet one more challenge before we can pull the trick off in Animal Crossing. Because of the distortion introduced by the camera perspective, it's not always obvious when the shadow of an object reaches its minimum in the game. That is, until you have _playground gym_.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/002.jpg" />
</div>

This baby will set you back 3000 Nook Miles, but oh-my-lord is it worth it. Since I am reasonably confident that it's made of little cubes, the playground gym forms some kind of oblique coordinate system when being placed on the ground.

## Putting It All Together

