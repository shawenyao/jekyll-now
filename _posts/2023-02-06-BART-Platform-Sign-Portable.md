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

An authentic BART experience that you can (literally) put on your desktop.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Raspberry Pi/picow&oled.png" />
</div>

_Image created by author on Google Slides. Left: Raspberry Pi Pico W; right: 128x64 OLED Display._

<br>

I like commuting by BART. It's fast, reliable and (relatively) carefree. Especially for its asking price, there isn't really a whole lot to complain about.

Authenticity would be another appeal. Wouldn't be so cool if the portable sign looks and feels just like the original?

## BART Platform Sign, the Original

Behold the original, real BART platform sign, a piece of display that looks all too familiar in the eyes of the 145,700 riders (as of [Q3 2022](https://en.wikipedia.org/wiki/Bay_Area_Rapid_Transit)) everyday.

Generally, the sign loops through four different layouts. First, there's the estimated wait time screen between trains, which can span multiple screens by itself. This is often followed by a second type of display, BART Service Advisories, usually regarding an annoucement of a train outage, cancellation, or just a friendly reminder from the police asking you to pay attention to your belongings. Third, a full-screen display of the destination kicks in when a train enters a platform. Finally, a digital clock pops up from time to time.

## Display Setup

There are many affordable options when it comes to adding a display to a Raspberry Pi. For example, this 0.96-inch one can be had for about [$3 apiece](https://www.amazon.com/gp/product/B09T6SJBV5/). It features an 128x64 OLED display and should provide enough screen real estate for all the important information to be shown.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/Raspberry Pi/picow&oled2.png" />
</div>

For a detail instruction on how to setup the display, here is an excellent [guide](https://www.tomshardware.com/how-to/oled-display-raspberry-pi-pico) from Tom's Hardware.

## Getting Real-Time Depature Estimates

BART offers real-time depature estimates via its [API](https://api.bart.gov/). A simple HTTPS request to:

```
https://api.bart.gov/api/etd.aspx?cmd=etd&orig={station}&dir={direction}&key={key}&json=y
```

will result in a list of incoming trains for a given station in a given direction being returned. This would have been a breeze if not for one caveat. For some reason, the official `urequests` library that comes with the MicroPython firmware has HTTP/1.0 hardcoded. Cloudflare, by which the domain `bart.gov` is protected, doesn't like it very much and will instantly shut down any connection attempt as such. This calls for a modification in the `request()` function in `urequests`. Fortunately, after playing with the script, I realize that the fix could be something as simple as changing [line 94](https://github.com/micropython/micropython-lib/blob/master/python-ecosys/urequests/urequests.py#L94) from:

```python
s.write(b"%s /%s HTTP/1.0\r\n" % (method, path))
```

to:

```python
s.write(b"%s /%s HTTP/1.1\r\n" % (method, path))
```

in addition to a few touches at the end to parse the JSON response correctly.

## Controlling Text Sizes

Without an operating system, changing text fonts or sizes isn't as straightforward. To solve the problem, Peter Hinch has developed a wonderful [solution](https://github.com/peterhinch/micropython-font-to-py), which to my understanding involves some sort of character-by-character images of the font that are cleverly encoded in a bytearray form. Once the `Writer` class is initialized with such bytearray:

```python
# various fonts
font6_writer = writer.Writer(oled, font6, verbose=False)
font10_writer = writer.Writer(oled, font10, verbose=False)
courier20_writer = writer.Writer(oled, courier20, verbose=False)
```

it can then be used to print arbitrary text to the OLED screen:

<p float="left" align="middle">
  <img src="https://shawenyao.github.io/Photos/BART-OLED/arriving.jpg" width="49%" />
  <img src="https://shawenyao.github.io/Photos/BART-OLED/schedule.jpg" width="49%" /> 
</p>

## Displaying Time

A Raspberry Pi Pico W doesn't have an internal battery to keep the clock running constantly, so we will need an authority to tell time upon boot up. This requires a call to `worldtimeapi.org`, where it will automatically deal with timezone conversion depending on user's IP:

```
https://worldtimeapi.org/api/ip
```

or fix the timezone with something like:

```
https://worldtimeapi.org/api/timezone/America/Los_Angeles
```

The response contains a JSON with all the information necessary to set the initial value of the onboard real time clock on a Raspberry Pi Pico W.

```python
# set initial time based on worldtimeapi.org
rtc = machine.RTC()
rtc.datetime((year, month, day, weekday, hours, minutes, seconds, subseconds))
```

After initialization, `rtc.datetime()` will return the current date and time.

<p float="left" align="middle">
  <img src="https://shawenyao.github.io/Photos/BART-OLED/clock.jpg" width="49%" />
</p>

## Putting It All Together

<div align="center">
  <img src="https://shawenyao.github.io/Photos/BART-OLED/demo.gif" style="width:100%;height:auto;"/>
</div>

## Appendix
### Code Repository
[https://github.com/shawenyao/bart-oled](https://github.com/shawenyao/bart-oled)