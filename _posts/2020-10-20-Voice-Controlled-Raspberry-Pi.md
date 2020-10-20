---
layout: post
title: Vocie-Controlled Raspberry Pi
tag:
  - bash
  - retropie
  - raspberry pi
comments: true
draft: true
berry: true
new: true
---

An end-to-end tutorial.

* [Google Assistant](https://assistant.google.com/) (or any voice assistant that IFTTT supports)
* [IFTTT](https://ifttt.com/)
* [Webhook](https://github.com/adnanh/webhook)
* [Webhook Relay](https://webhookrelay.com/) (optional)


## Webhook
/etc/webhook.conf
```json
[
  {
    "id": "pictrl",
    "execute-command": "/usr/local/bin/pictrl",
    "command-working-directory": "/home/pi/Webhooks",
    "pass-arguments-to-command":
    [
      {
        "source": "query",
        "name": "action"
      }
    ],
    "trigger-rule":
    {
      "match":
      {
        "type": "value",
        "value": "secret",
        "parameter":
        {
          "source": "url",
          "name": "token"
        }
      }
    }
  }
]
````

start as a service
```bash
sudo systemctl start webhook
```

auto-start as a service on boot
```bash
sudo systemctl enable webhook
```

/usr/local/bin/pictrl
```sh
#!/bin/sh
action=$1

if [ "$action" = "play" ]
then
  kodi-send --action="PlayerControl(play)"
fi
```

http://ipaddress:port/hooks/pictrl?token=secretw&action=play
