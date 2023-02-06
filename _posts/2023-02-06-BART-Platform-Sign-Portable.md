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

## Getting Real-Time Depature Estimates

```
https://api.bart.gov/api/etd.aspx?cmd=etd&orig=MONT&dir=n&key=xxx&json=y
```

```python
s.write(b"%s /%s HTTP/1.0\r\n" % (method, path))
```

```python
s.write(b"%s /%s HTTP/1.1\r\n" % (method, path))
```

## Controlling Text Sizes

## Displaying Time

```
https://worldtimeapi.org/api/ip
```

## Demo

<div align="center">
  <img src="https://shawenyao.github.io/Photos/BART-OLED/demo.gif" style="width:100%;height:auto;"/>
</div>

## Appendix
### Code Repository
[https://github.com/shawenyao/bart-oled](https://github.com/shawenyao/bart-oled)
