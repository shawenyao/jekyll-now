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

all too familiar.

Authenticity would be another appeal. Wouldn't be so cool if the portable sign looks and feels just like the original?

## BART Platform Sign, the Original

Generally, the original BART platform sign loops through four different layouts. First, there's the estimated wait time screen between trains, which can span multiple screens by itself. This is often followed by a second type of display, BART Service Advisories, usually regarding an annoucement of a train outage, cancellation, or just a friendly reminder from the police asking you to pay attention to your belongings. Third, a full-screen display showing the destination kicks in when a train enters a platform. Finally, a digital clock pops up from time to time.

## Display Setup


## Getting Real-Time Depature Estimates

BART offers real-time depature estimates via its API. 

```
https://api.bart.gov/api/etd.aspx?cmd=etd&orig={station}&dir={direction}&key={key}&json=y
```

This would have been a breeze, if not for one caveat. For some reason, the official `urequests` library that comes with the MicroPython firmware has HTTP/1.0 hardcoded. Cloudflare, by which the domain `bart.gov` is protected, doesn't like it very much and will instantly shut down any connection attempt as such. This calls for a modification in the `request()` function in `urequests`. Fortunately, after playing with the script, I realize that the fix could be something as simple as changing [line 94](https://github.com/micropython/micropython-lib/blob/master/python-ecosys/urequests/urequests.py#L94) from:

```python
s.write(b"%s /%s HTTP/1.0\r\n" % (method, path))
```

to:

```python
s.write(b"%s /%s HTTP/1.1\r\n" % (method, path))
```

in addition to a few touches at the end to parse the JSON response correctly.

## Controlling Text Sizes

Changing the font size can be without an operating system, bytearray

```python
# various fonts
font6_writer = writer.Writer(oled, font6, verbose=False)
font10_writer = writer.Writer(oled, font10, verbose=False)
courier20_writer = writer.Writer(oled, courier20, verbose=False)
```

## Displaying Time

A Raspberry Pi Pico W doesn't have an internal battery to keep the clock running constantly, so we will need an authority to tell time upon boot up. This requires a call to `worldtimeapi.org`, where it will automatically deal with timezone conversion depending on user's IP:

```
https://worldtimeapi.org/api/ip
```

The response contains a JSON with all the information necessary to set the initial value of the onboard real time clock on a Raspberry Pi Pico W.

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
