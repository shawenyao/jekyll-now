---
layout: post
title: A Distributed Motion-Sensitive Lighting System
tag:
  - raspberry pi
  - smart home
  - python
comments: true
draft: True
berry: true
new: true
---

Fiat lux.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Raspberry Pi/all.png" />
</div>

_Image created by author using Google Slides. Left: Raspberry Pi 4 Model B; right: Raspberry Pi Pico W._

<br>

## Design 1: Motion Sensor 101

<div align="center">
  <img src="https://shawenyao.github.io/Photos/light/1.png" />
</div>

## Design 2: Distributed Motion Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/light/2.png" />
</div>

## Design 3: Coordinating the Sensors

There is an obvious problem with the previous design. The fact that the two sensors work independently and memoryless means once the light is turned on, further movement cannot extend the duration of the lightning.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/light/problem.png" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/Photos/light/3.png" />
</div>

## Life Hack

## Appendix

