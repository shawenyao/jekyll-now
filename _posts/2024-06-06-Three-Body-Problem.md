---
layout: post
title: Three-Body Problem
tag:
  - raspberry pi
  - maths
  - python
comments: true
draft: False
berry: true
new: True
---

Planetary motions on a microcontroller.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Three-Body/image.png" style="width:100%;height:auto;"/>
</div>

## Requirements
* [Raspberry Pi Pico](https://www.raspberrypi.com/products/raspberry-pi-pico/) x 1
* Breadboard x 1
* Male-to-male jump wires x 4
* 128x64 OLED Display x 1
* Micro-USB  cable x 1
* Power adapter or power bank x 1

## Instructions
* Connect the OLED display to the Raspberry Pi Pico on a breadboard
* Download and flash the [MicroPython firmware](https://github.com/v923z/micropython-builder/releases)
* Copy [main.py](https://github.com/shawenyao/three-body/blob/main/main.py) onto the Raspberry Pi Pico
* Connect the Raspberry Pi Pico to a power source

## Putting It All Together

<video src="https://shawenyao.github.io/Photos/Three-Body/demo.mp4" controls="controls" width="100%"></video>

## References
* Problem overview by [Wikipedia](https://en.wikipedia.org/wiki/Three-body_problem)
* Python solution by [Benjamin Badge](https://blbadger.github.io/3-body-problem.html)
* Initial conditions based on [Ricky Reusser](https://observablehq.com/@rreusser/periodic-planar-three-body-orbits)
