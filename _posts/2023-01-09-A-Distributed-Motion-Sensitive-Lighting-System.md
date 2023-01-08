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

[Rasperry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi). The newest entry to the Raspberry Pi family, [Pico W](https://www.raspberrypi.com/news/raspberry-pi-pico-w-your-6-iot-platform/).

Smart plug. For example, [Kasa](https://www.kasasmart.com/us/products/smart-plugs).

Last but certainly not least, there's the motion sensor itself. I am using the HC-SR505 senor, a type of [passive infrared (PIR) sensor](https://en.wikipedia.org/wiki/Passive_infrared_sensor).

## Design 1: Motion Sensing 101

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/1.png" />
</div>

## Design 2: Distributed Motion Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/2.png" />
</div>

There is an obvious problem with the previous design. The fact that the two sensors work independently and memoryless means once the light is turned on, further movement cannot extend the duration of the lightning.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/problem.png" />
</div>

## Design 3: Coordinating the Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/3.png" />
</div>

## Life Hacks

False trigger. 

Cats.

## Appendix

