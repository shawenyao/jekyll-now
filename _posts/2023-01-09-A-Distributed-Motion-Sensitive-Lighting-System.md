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

_Image created by the author using Google Slides. Left: Raspberry Pi 4 Model B; right: Raspberry Pi Pico W._

<br>

Many. Ideally, the system should have low power consumption and offer on-the-go configurability.

## Smart Home Basics

## Design 1: Motion Sensor 101

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/1.png" />
</div>

## Design 2: Distributed Motion Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/2.png" />
</div>

## Design 3: Coordinating the Sensors

There is an obvious problem with the previous design. The fact that the two sensors work independently and memoryless means once the light is turned on, further movement cannot extend the duration of the lightning.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/problem.png" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/3.png" />
</div>

## Life Hacks

## Appendix

