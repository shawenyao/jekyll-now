---
layout: post
title: Homebrewing RetroPie
tag:
  - bash
  - retropie
  - raspberry os
comments: true
---

Customizing the launch sequence of RetroPie.

```bash
# /opt/retropie/configs/all/autostart.sh

# press ctrl + d will automatically launch this script in terminal
# making it a useful hub for executing more "wordy" commands

# note that actually, anykey other than the pre-defined ones will abort
echo "==================================================================="
echo "=== EmulationStation starting in 3 seconds. Press "z" to abort. ==="
echo "==================================================================="

# read 1 character from input with a 3-second timeout 
# and save in variable $input
read -n 1 -t 3 input
echo ""

# default case
# if the input is empty or time runs out, start emulation station
# works without keyboard, e.g., when only controller is connected
# in case keyboard is indeed conncected, hit enter or space to skip the wait
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

