---
layout: post
title: BART Platform Sign Portable
tag:
  - raspberry pi
  - smart home
  - python
comments: true
draft: True
berry: true
new: true
---

BART PSP™.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Raspberry Pi/picow&oled.png" />
</div>

_Image created by author on Google Slides. Left: Raspberry Pi Pico W; right: 128x64 OLED Display._

<br>

Authenticity would be another appeal. Wouldn't be so cool if the portable sign looks and feels just like the original?

## BART Platform Sign, the Original

## Getting Real-Time Depature Estimates

```
https://api.bart.gov/api/etd.aspx?cmd=etd&orig=MONT&dir=n&key={api_key}&json=y
```

For some reason, the official `urequests` library that comes with the MicroPython firmware has HTTP/1.0 hardcoded. Cloudflare (by which the domain `bart.gov` is protected) doesn't like it and will instantly shut down any connection request as such. This calls for a fix in the `request()` function in `urequests`. In fact, it could be as something simple as changing [line 94](https://github.com/micropython/micropython-lib/blob/master/python-ecosys/urequests/urequests.py#L94) from

```python
s.write(b"%s /%s HTTP/1.0\r\n" % (method, path))
```

to

```python
s.write(b"%s /%s HTTP/1.1\r\n" % (method, path))
```

in addition to a few touches at the end to parse the JSON response correctly.

## Controlling Text Sizes

```python
# various fonts
font6_writer = writer.Writer(oled, font6, verbose=False)
font10_writer = writer.Writer(oled, font10, verbose=False)
courier20_writer = writer.Writer(oled, courier20, verbose=False)
```

## Displaying Time

A Raspberry Pi Pico W doesn't have an internal battery to keep the clock running after power off, so without 

```
https://worldtimeapi.org/api/ip
```

The response contains information needed to set the initial value of the onboard real time clock.

```python
# set initial time based on worldtimeapi.org
rtc = machine.RTC()
rtc.datetime((year, month, day, weekday, hours, minutes, seconds, subseconds))
```

After initialization, `rtc.datetime()` will return the current date and time.

## Putting It All Together

<div align="center">
  <img src="https://shawenyao.github.io/Photos/BART-OLED/demo.gif" style="width:100%;height:auto;"/>
</div>

## Appendix
### Code Repository
[https://github.com/shawenyao/bart-oled](https://github.com/shawenyao/bart-oled)
