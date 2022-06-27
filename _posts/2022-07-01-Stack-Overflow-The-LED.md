---
layout: post
title: Stack Overflow The LED
tag:
  - windows
  - smart home
comments: true
draft: true
keyboard: true
new: true
---

* [Stack Overflow The Key](https://drop.com/buy/stack-overflow-the-key-v2-macropad): A Stack-Overflow-branded macropad with 3 buttons that's (by default) capable of performing copy and paste (CTRL, C and V). V2 added RGB support.
* [QMK (Quantum Mechanical Keyboard)](https://docs.qmk.fm/#/): An open-source mechanical keyboard protocol.
* [Vial](https://get.vial.today/): An QMK fork with a GUI for configuration.
* [Windows Runtime (WinRT)](https://en.wikipedia.org/wiki/Windows_Runtime): A set of Windows APIs.

## Controlling Lighting

## Listening to Notifications

## Putting It All Together

## References

## Appendix
### Install all the software packages mentioned above
```bash
pip install hid
pip install winrt
```

### Configure hid
Download the latest release of `hidapi-win.zip` from [GitHub](https://github.com/libusb/hidapi/releases), unzip and put `x64/hidapi.dll` into `C:\Windows\System32`
