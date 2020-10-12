---
layout: post
title: Homebrewing RetroPie
tag:
  - bash
  - retropie
  - raspberry pi
comments: true
keyboard: true
---

Customizing the launch sequence of RetroPie.

```bash
# /opt/retropie/configs/all/autostart.sh

# purposes: 
# 1) upon boot up, wait for user input to decide what to launch
# 2) by default, empty input or time out will launch emulation station
# 3) also useful after boot up, since pressing ctrl + d automatically runs
# this script from the shell, it makes for a powerful hub for executing more
# "wordy" commands. for example, ctrl + d then s will shut the system down

# note that actually, any key other than the pre-defined ones will abort
echo "================================================================="
echo "=== EmulationStation starting in 3 seconds. Press z to abort. ==="
echo "================================================================="

# read 1 character from input with a 3-second timeout 
# and save in variable $input
read -n 1 -t 3 input
echo ""

# default case
# if the input is empty or time runs out, start emulation station
# this works without keyboard, e.g., when only controller is connected
# in case keyboard is indeed connected, hit enter or space to skip the wait
if [ -z "$input" ]
then
    emumlationstation

# if "x", then start desktop
elif [ "$input" == "x" ]
then
    startx

# the rest is for illustrative purposes
# if "s", then shutdown
elif [ "$input" == "s" ]
then
    sudo shutdown now

# if "r", then reboot
elif [ "$input" == "r" ]
then
    sudo reboot

# if "k", then start kodi
elif [ "$input" == "k" ]
then
    kodi

# if anything else, print help info
else
    # print help info
fi
```

