---
layout: post
title: A Distributed Motion-Controlled Lighting System
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

While [voice control](https://www.shawenyao.com/Voice-Controlled-Raspberry-Pi/) already works decently well, motion control is arguably the more natural way of interacting with certain appliances. Ideally, the system should have low power consumption and offer on-the-go configurability.

## Smart Home Basics

For this project, we will be relying on various [Rasperry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi) computers. The 4th generation, Raspberry Pi 4 Model B, is by far the most powerful Raspberry Pi with a quad-core CPU clocking in at 1.5GHz. The newest entry to the Raspberry Pi family, [Pico W](https://www.raspberrypi.com/news/raspberry-pi-pico-w-your-6-iot-platform/), is a microcontroller capable of of running [MicroPython](https://en.wikipedia.org/wiki/MicroPython) and accessing the Internet, and will be serving as the bridge between the main Raspberry Pi unit and the motion sensor.

Smart plugs are next. These are essentially Wi-Fi-enabled switches that can be turned on or off via an API, rendering non-smart devices such as a floor lamp "smart". For example, TP-Link offers many choices under the brand [Kasa](https://www.kasasmart.com/us/products/smart-plugs). Programmatic control of the Kasa smart plugs is made possible by the [python-kasa](https://github.com/python-kasa/python-kasa) library.

Last but certainly not least, there's the motion sensor itself. The HC-SR505 senor, a type of [passive infrared (PIR) sensor](https://en.wikipedia.org/wiki/Passive_infrared_sensor), can get the job done nicely.

## Design 1: Motion Sensing 101

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/1.png" />
</div>

The most straightforward solution is probably a two-Pi system. The first unit, a Pico W connected to a PIR motion sensor and placed at the bottom of the stairs, is responsible for detecting motion. If and when it does, the microcontroller sends a signal wirelessly to the second unit, a Raspberry Pi 4 listening to such request via a Flask server, who then turns on the light, wait a bit and switches off the light. A detailed guide on how to make a Pico work with a HC-SR505 sensor can be found at [freva.com](https://www.freva.com/pir-motion-sensor-on-a-raspberry-pi-pico/).

From a human-machine interface standpoint, anyone who wishes to go upstairs simply need to proceed as usual. The action will be captured at the very beginning of the climb so lighting will hopefully be available for the majority of the journey. The duration of the lighting is controlled by the server side and should be reasonably long (say a minute) to allow sufficient time for climbing before darkness falls again. When it times out, the server tells the light to power off.

Currently, the second Pi is a must because the MicroPython environment available on the Pico W has yet to support the python-kasa library. This is not necessarily a bad thing. In fact, it must be taken into account that upgrading code on a Raspberry Pi Pico W is nontrivial. It requires physically connecting the board to a computer, launching an editor, editing and saving. Therefore, it's advisable to keep the logic on the Pico W as simple and generic as possible, and leave the more complicated part to the more powerful (and better-supported) Raspberry Pi 4.

## Design 2: Distributed Motion Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/2.png" />
</div>

Now, the light turns on when I go upstairs - that's all good. But sooner or later, I inevitably need to come downstairs and wish the light turned on as well. So comes a third unit, another Raspberry Pico W placed at the top of the stairs. Everything that worked before should continue to work with the same setup and the same code, only that now there are two triggers. When I go upstairs, the bottom sensor detects me and turns on the light. In a few seconds, the sensor upstairs also sees me and wants to turn on the light, but it doesn't matter as the light is already on - vice versa. Moreover, the system can scale easily - any number of additional Pico W/PIR sensor can be added or removed.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/problem.png" />
</div>

There is a problem with such design, however. The fact that the two sensors work **independently** and **memorylessly** also brings a pretty serious inconvenience. If I decide to stay on the stairs, there's no way for the system to extend the duration of the lighting. For instance, after my movement is picked up by the first sensor, the light is set to stay on for a predetermined amount of time, however generous that amount is. Even if another sensor (or the same one, for the matter) detects further motion, its signal will be useless since it merely tries to turn on a light that is already on, or off when it's already off. The design calls for an upgrade.

## Design 3: Coordinating the Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/3.png" />
</div>



## Life Hacks

False trigger. 

Cats.

## Appendix
* [Repository](https://github.com/shawenyao/light)
