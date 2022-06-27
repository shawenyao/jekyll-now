---
layout: post
title: Stack Overflow The LED
tag:
  - windows
  - python
  - smart home
comments: true
draft: false
keyboard: true
new: true
---

Good artists copy. Great artists steal. Greatest artists copy, then paste.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/TheKeyV2/logo.jpg" />
</div>

Originally inspired by a meme, Stack Overflow recently started shipping for its `The Key V2` macropad. On top of the signature 3-button layout, V2 added support for RGB lightning, enabling it to function not only as an input device but an output one as well. In this post, we are going to **let the keyboard shine whenever there are any unread notifications**.

A quick rundown of all the mumbo jumbos:
* [Stack Overflow The Key](https://drop.com/buy/stack-overflow-the-key-v2-macropad): A Stack-Overflow-branded macropad with 3 buttons, dedicated to performing copy and paste by default (i.e., CTRL, C and V). V2 added RGB support.
* [QMK (Quantum Mechanical Keyboard)](https://docs.qmk.fm/#/): An open-source protocol adopted by a variety of mechanical keyboards.
* [Vial](https://get.vial.today/): An QMK fork that comes with a GUI and easier configurability.
* [HID (Human Interface Device)](https://en.wikipedia.org/wiki/Human_interface_device): A USB protocol to send information between input devices and computers. Also, a Python package by the same name.
* [Windows Runtime (WinRT)](https://en.wikipedia.org/wiki/Windows_Runtime): A set of Windows APIs.

## Controlling Lighting

Reinventing the communication protocol between a PC and a keyboard isn't fun. Fortunately, the Vial project already had it all figured out (see appendix). After flashing the keyboard with the Vial-compatible firmware (again, see appendix), a very specific message needs to be sent by the Python script to control the lighting on the keyboard:

```python
import hid
import struct

# constants
CMD_VIA_LIGHTING_SET_VALUE = 0x07
QMK_RGBLIGHT_EFFECT = 0x81
MSG_LEN = 32

# hid device path
# use hid.enumerate() to figure out
PATH = b'\\\\?\\HID#VID_FEED&PID_6070&MI_01#7&36c4d81a&0&0000#{4d1e55b2-f16f-11cf-88cb-001111000030}'

# example: change RGB mode to 14 (Rainbow Swirl)
mode = 14
msg = struct.pack(">BBB", CMD_VIA_LIGHTING_SET_VALUE, QMK_RGBLIGHT_EFFECT, mode)
msg += b"\x00" * (MSG_LEN - len(msg))
dev = hid.Device(path=PATH)
dev.write(b"\x00" + msg)
dev.close()
```

Mode 14 happens to be Rainbow Swirl. It has an eye-catching animation with plenty of colors, which makes it hard to ignore - an ideal candidate for the notification mode. 

As for the HID device path, my keyboard actually gave me four instances as `hid.enumerate()` suggested. Only one works - be prepared to find the right path by elimination.

## Listening to Notifications

There's probably no better way to get the system-wide notification status than to ask the system itself. The `WinRT` APIs, accessible in Python via the `pywinrt` package, makes it possible.

```python
from winrt.windows.ui.notifications.management import UserNotificationListener
from winrt.windows.ui.notifications import NotificationKinds

# ask windows how many notifications there are currently
listener = UserNotificationListener.get_current()
notifications = await listener.get_notifications_async(NotificationKinds.TOAST)
print(len(notifications))
```

## Putting It All Together
The remaining to-dos include putting the listener in a loop and checking for status update every couple seconds. Depending on whether there are unread notifications or not, send the message to the keyboard in order to adjust RGB mode accordingly. See appendix for the full script.

```python
# turn off notification mode upon initialization
notification_mode = False
toggle_notification_mode(on=notification_mode)

while True:
    time.sleep(1)

    # ask windows how many notifications there are currently
    listener = UserNotificationListener.get_current()
    notifications = await listener.get_notifications_async(NotificationKinds.TOAST)

    # if there is at least one notification and the LED is not in notification mode
    if len(notifications) >= 1 and notification_mode == False:
        # turn on notification mode
        notification_mode = True
        toggle_notification_mode(on=notification_mode)

    # if there isn't any notification and the LED is in notification mode
    elif len(notifications) == 0 and notification_mode == True:
        # turn off notification mode
        notification_mode = False
        toggle_notification_mode(on=notification_mode)
```

Finally, enjoy!

<div align="center">
  <img src="https://shawenyao.github.io/Photos/TheKeyV2/demo.gif" style="width:100%;height:auto;"/>
</div>

## References
* [Vial-compatible firmware for Stack Overflow The Key V2 by JetSerge](https://drop.com/buy/stack-overflow-the-key-v2-macropad/talk/2892369)
* [Vial source code](https://github.com/vial-kb/vial-gui)
* [How can I listen to Windows 10 notifications in Python?](https://stackoverflow.com/questions/64043297/how-can-i-listen-to-windows-10-notifications-in-python)
* [Working example](https://github.com/shawenyao/the_key_v2/blob/main/control_leds.py)

## Appendix
### Install all the software packages mentioned above
```bash
pip install hid
pip install winrt
```

### Configure hid
Download the latest release of `hidapi-win.zip` from [GitHub](https://github.com/libusb/hidapi/releases), unzip and put `x64/hidapi.dll` into `C:\Windows\System32`
