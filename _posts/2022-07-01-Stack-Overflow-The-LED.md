---
layout: post
title: Stack Overflow The LED
tag:
  - windows
  - python
  - smart home
comments: true
draft: true
keyboard: true
new: true
---

* [Stack Overflow The Key](https://drop.com/buy/stack-overflow-the-key-v2-macropad): A Stack-Overflow-branded macropad with 3 buttons, dedicated to performing copy and paste by default (i.e., CTRL, C and V). V2 added RGB support.
* [QMK (Quantum Mechanical Keyboard)](https://docs.qmk.fm/#/): An open-source protocol to configure mechanical keyboard.
* [Vial](https://get.vial.today/): An QMK fork that comes with a GUI.
* [Windows Runtime (WinRT)](https://en.wikipedia.org/wiki/Windows_Runtime): A set of Windows APIs.

## Controlling Lighting

Reinventing the communication protocol between a PC and a keyboard isn't fun. Gladly, the Vial project already had it all figured out (see appendix). To control the lighting on the keyboard, a very specific message needs to be sent by the Python script:

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

Mode 14 happens to be Rainbow Swirl. It has an eye-catching animation with plenty of colors, which makes it hard to ignore - an ideal candidate for notification purposes. We will call it the notification mode going forward.

## Listening to Notifications

There's probably no better way to get the system-wide notification status than to ask the system itself. The `WinRT` APIs, accessible in Python via the `pywinrt` package makes it possible.

```python
from winrt.windows.ui.notifications.management import UserNotificationListener
from winrt.windows.ui.notifications import NotificationKinds

# ask windows how many notifications there are currently
listener = UserNotificationListener.get_current()
notifications = await listener.get_notifications_async(NotificationKinds.TOAST)
print(len(notifications))
```

## Putting It All Together
The final thing to do is to put the listener in a loop, check for states every couple seconds and depending on whether there are unread notifications or not, adjust RGB mode accordingly.

```python
# turn off notification mode upon initialization
notification_mode = False
toggle_notification_mode(on=notification_mode)

while True:
    time.sleep(1)

    # ask windows how many notifications there are currently
    listener = UserNotificationListener.get_current()
    notifications = await listener.get_notifications_async(NotificationKinds.TOAST)

    # if there is any notification and the LED is not in notification mode
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

## References
* [Vial-compatible firmware for Stack Overflow The Key V2 by JetSerge](https://drop.com/buy/stack-overflow-the-key-v2-macropad/talk/2892369)
* [Vial source code](https://github.com/vial-kb/vial-gui)
* [How can I listen to Windows 10 notifications in Python?](https://stackoverflow.com/questions/64043297/how-can-i-listen-to-windows-10-notifications-in-python)

## Appendix
### Install all the software packages mentioned above
```bash
pip install hid
pip install winrt
```

### Configure hid
Download the latest release of `hidapi-win.zip` from [GitHub](https://github.com/libusb/hidapi/releases), unzip and put `x64/hidapi.dll` into `C:\Windows\System32`
