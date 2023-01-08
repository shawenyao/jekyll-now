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

[Rasperry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi). The 4th generation, Raspberry Pi 4 Model B, is by far the most powerful Raspberry Pi with a quad-core CPU running at 1.5GHz. The newest entry to the Raspberry Pi family, [Pico W](https://www.raspberrypi.com/news/raspberry-pi-pico-w-your-6-iot-platform/), is a microcontroller capable of of running [MicroPython](https://en.wikipedia.org/wiki/MicroPython) and access the Internet.

Smart plugs come next. These are essentially Wi-Fi-enabled switches that can be turned on or off via an API, rendering non-smart devices such as a floor lamp "smart". For example, TP-Link offers many choices under the brand [Kasa](https://www.kasasmart.com/us/products/smart-plugs). Programmatic control of the Kasa smart plugs is made possible by the [python-kasa](https://github.com/python-kasa/python-kasa) library.

Last but certainly not least, there's the motion sensor itself. The HC-SR505 senor, a type of [passive infrared (PIR) sensor](https://en.wikipedia.org/wiki/Passive_infrared_sensor), gets the job done nicely.

## Design 1: Motion Sensing 101

A detailed guide can be found at [freva.com](https://www.freva.com/pir-motion-sensor-on-a-raspberry-pi-pico/).

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/1.png" />
</div>

## Design 2: Distributed Motion Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/2.png" />
</div>

There is an obvious problem with such design. The fact that the two sensors work independently and memoryless means once the light is turned on, further movement cannot extend the duration of the lightning.

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

