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

I've been playing _Animal Crossing: New Horizons_, where my in-game character flew to a deserted island in order to start a new life. Despite its cartoony art style, the game manages to establish a remarkable degree of realism, to the point where it almost feels like a living and breathing world. For example, I know for a fact that my island exists somewhere in the northern hemisphere; I know that the sun rises and sets there every real-world day; I know that the seasons rotate and spring is coming. At some point, I began to wonder how much further I can push this, e.g., given what's observable in the game, can I deduce where my island is? If so, where might it be?

In this post, please join me for a tour to my island, and I will unveil its location at the end (sort of).

## The Longitude
This is an easy one. Due to the fact that the game runs on real-world clock, my deserted island has to be conveniently located in the same time zone as where I physically am (or at least wherever my system is set). Voila! There it is and it can't be too far off.

## The Latitude
Unlike the previous case, figuring out the latitude can get a little tricky. In a nutshell, it boils down to measuring the _solar elevation angle_ at _solar noon_. Astronomy tells us that the following equation holds true:

$$
h = 90^\text{o} - \left| \phi - \delta \right|
$$

where
* $h$ is the solar elevation angle at solar noon. It is also the angle between a ray of sunlight and the horizon at the observation point and can be found by taking inverse tangent on the ratio of the height of an object over the length of its shadow. In addition, solar noon is defined as the time of the day when the Sun reaches the highest point. Note that this is equivalent to the length of shadow being the shortest, and it doesn't necessarily coincide with 12pm.
* $\phi$ is the latitude of the observation point (a positive number in this case)
* $\delta$ is the latitude of the subsolar point (a negative number in this case), also know as the solar declination angle.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/animal_crossing/1_label.png" />
</div>

For full reference, see [here](https://en.wikipedia.org/wiki/Solar_zenith_angle), [here](https://commons.wvc.edu/rdawes/ASTR217/Gnomon.pdf) and [here](https://vortex.plymouth.edu/sun/sun4a.html).

There's yet one more challenge before we can pull this off in Animal Crossing. Because of the distortion introduced by the camera perspective, it's not always obvious when the shadow of an object reaches its minimum in the game. That is, until you can afford a _playground gym_.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/002.jpg" />
</div>

This baby will set you back 3000 Nook Miles, but oh-my-lord is it worth every mile. Since I am reasonably confident that it's made of little cubes, the playground gym forms some kind of _orthonormal basis_ in a three-dimensional coordinate system when being placed on the ground, allowing distance to be estimated reliably on a relative basis.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/003.jpg" />
</div>

The rest is straightforward but definitely not trivial. While my in-game character sat on the swing, I started to capture the gameplay footage every two minutes around noon, calculated the length of the shadow, found the minimum and derived the solar elevation angle $h$.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Animal Crossing/004.jpg" />
</div>

$$
h = \arctan{ \frac{ 4.9079 } { 3.5735 } } = 26.9706^\text{o}
$$

From [here](https://rl.se/sub-solar-point), I know that the solar declination angle $\delta$ is $+7.9^\text{o}$ today. Finally, the latitude of my island is given by:

$$
\phi = 90^\text{o} - h + \delta = 70.9294^\text{o}
$$

## Putting It All Together

Now we get to observe where my island is on the globe, along with that of any other Animal Crossing players whose island also happens to be in the northern hemisphere.

<iframe src="https://shawenyao.github.io/R/output/animal_crossing/my_island.html" style="border:none;height:300px;width:100%;" scrolling="no"></iframe>

But there's a slight problem. There isn't any island there!
