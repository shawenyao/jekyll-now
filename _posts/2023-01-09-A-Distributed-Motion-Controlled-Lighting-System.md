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

_Image created by author on Google Slides. Left: Raspberry Pi 4 Model B; right: Raspberry Pi Pico W._

<br>

I have been looking for the optimal, most hassle-free way to control my stairs light. The electrical engineers who designed the apartment apparently have put a great deal of thoughts into it, too. The dome lights above the stairs can be turned on or off by two switches on both ends in an "[exclusive or (XOR)](https://en.wikipedia.org/wiki/Exclusive_or)" fashion. The intention, if I may speculate, is for users to flip one switch (when going either up or down) to turn the light on, than the other (when finished) to turn it off. This is fine for most use cases, but it's not difficult to think of occasions where a handsfree approach would be preferred. While [voice control](https://www.shawenyao.com/Voice-Controlled-Raspberry-Pi/) already works decently well, a motion-controlled solution is arguably the more natural way of interaction in this case. The system should be able to monitor movement on the stairs, switching the light on or off accordingly. A low power consumption would be a nice feature as well, so it can last for days on a power bank. Ideally, I would also like to have on-the-fly configurability without rewiring, and some sort of resistance to unintended distractions (yes, I am looking at my [cat](https://www.shawenyao.com/Cat-in-Black/)).

## Smart Home Basics

For this project, I will be utilizing various [Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi) computers. The 4th generation, Raspberry Pi 4 Model B, is by far the most powerful Raspberry Pi with a quad-core CPU clocking in at 1.5GHz. The newest entry to the Raspberry Pi family, Pico W, is a microcontroller capable of running [MicroPython]([https://en.wikipedia.org/wiki/MicroPython](https://micropython.org/)) and accessing the Internet, and will be serving as the bridge between the main Raspberry Pi unit and the motion sensor.

Smart plugs are next. These are essentially Wi-Fi-enabled switches that can be turned on or off via an API, rendering non-smart devices such as a floor lamp "smart". For example, TP-Link offers many choices under the brand [Kasa](https://www.kasasmart.com/us/products/smart-plugs). Programmatic control of the Kasa smart plugs is made possible by the [python-kasa](https://github.com/python-kasa/python-kasa) library.

Last but certainly not least, there's the motion sensor itself. The HC-SR505 sensor, a type of [passive infrared (PIR) sensor](https://en.wikipedia.org/wiki/Passive_infrared_sensor) for instance, can get the job done nicely.

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

Now, the light turns on when I go upstairs - that's all good. But sooner or later, I might have to come downstairs and wish the light turned on as well. So comes a third unit, another Raspberry Pico W placed at the top of the stairs. Everything that worked before should continue to work with the same setup and the same code, only that now there are two triggers. When I go upstairs, the bottom sensor detects me and turns on the light. In a few seconds, the sensor upstairs also sees me and wants to turn on the light, but it doesn't matter as the light is already on - vice versa. Moreover, the system can scale easily - any number of additional Pico Ws/PIR sensors can be added or removed.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/problem.png" />
</div>

There is a problem with such design, however. The fact that the two sensors work _independently_ and _memorylessly_ brings a serious inconvenience. If I decide to stay on the stairs, there's no way for the system to extend the duration of the lighting. For example, after my movement is picked up by the first sensor, the light is set to stay on for a predetermined amount of time (however generous that amount is). Even if another sensor (or the same one, for the matter) detects further motion, its signal will be useless since it merely tries to turn on a light that is already on, or off when it's already off. The system calls for an upgrade.

## Design 3: Coordinating the Sensors

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/3.png" />
</div>

In the final design, the Pico Ws no longer assume to role of triggering the logic to control lights. Instead, they focus on one thing and one thing alone: sending the signals detected by the PIR sensor to the server. The server logs the timestamp at which the last motion is reported. A new process on the Raspberry Pi 4, an infinite loop, repeatedly triggers a piece of logic that compares the current time with the timestamp of last motion. If the difference is within the duration for which the light is meant to be turned on but the light is somehow off, it turns the light on. If the difference is greater than the duration but the light is on, it turns it off. In other words, the system has _memory_ now. As a result, any detected motion will reset the countdown to lights off, enabling a much more intuitive user experience.

## Demo



<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/demo.gif" style="width:100%;height:auto;"/>
</div>

## Life Hacks

In my experience, the PIR sensor is usually sensitive enough to real human movement (true positive). On the contrary, stairs light randomly turning on, especially at night, has become a bigger concern. Is it the cat? Should I call 911? Or, could it simply be a false positive? None of them seems a pleasant thought exactly. The situation persisted for a few nights, until -

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Light/hack.jpg" />
</div>

_Left: Raspberry Pi Pico W and HC-SR505 sensor; right: Raspberry Pi Pico W and HC-SR505 sensor with a scroll of paper._

<br>

To my great surprise, a simple scroll of paper works wonders at getting rid of the false alarms, by virtue of limiting the range of the sensor's visibility. Furthermore, ever since I accidentally left it pointing upward one time, the system has literally turned a blind eye to my cat's loitering - yet another unexpected but delightful side effect.

## Appendix
### Code repository
[https://github.com/shawenyao/light](https://github.com/shawenyao/light)
