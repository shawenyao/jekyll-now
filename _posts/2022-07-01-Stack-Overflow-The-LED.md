---
layout: post
title: Stack Overflow The LED
tag:
  - windows
  - smart home
comments: true
draft: false
keyboard: true
new: true
---

* [Stack Overflow The Key](https://drop.com/buy/stack-overflow-the-key-v2-macropad): A Stack-Overflow-branded macropad with 3 buttons, dedicated to performing copy and paste by default(i.e., CTRL, C and V). V2 added RGB support.
* [QMK (Quantum Mechanical Keyboard)](https://docs.qmk.fm/#/): An open-source protocol to configure mechanical keyboard.
* [Vial](https://get.vial.today/): An QMK fork that comes with a GUI.
* [Windows Runtime (WinRT)](https://en.wikipedia.org/wiki/Windows_Runtime): A set of Windows APIs.

## Controlling Lighting

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

# change RGB mode to 2 (breathing)
mode = 2
msg = struct.pack(">BBB", CMD_VIA_LIGHTING_SET_VALUE, QMK_RGBLIGHT_EFFECT, mode)
msg += b"\x00" * (MSG_LEN - len(msg))
dev = hid.Device(path=PATH)
dev.write(b"\x00" + msg)
dev.close()
```

## Listening to Notifications

```python
from winrt.windows.ui.notifications.management import UserNotificationListener
from winrt.windows.ui.notifications import NotificationKinds

# ask windows how many notifications there are
listener = UserNotificationListener.get_current()
notifications = await listener.get_notifications_async(NotificationKinds.TOAST)
print(len(notifications))
```

## Putting It All Together

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
