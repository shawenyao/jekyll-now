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

> “Any sufficiently advanced technology is indistinguishable from magic.”
> ― Arthur C. Clarke, Profiles of the Future: An Inquiry Into the Limits of the Possible

* [Raspberry Pi](https://www.raspberrypi.org/)
* [Webhook](https://github.com/adnanh/webhook)
* [Port Forwarding](https://en.wikipedia.org/wiki/Port_forwarding) or [Webhook Relay](https://webhookrelay.com/)
* [FreeDNS](https://freedns.afraid.org/dynamic/)
* [IFTTT](https://ifttt.com/)
* [Google Assistant](https://assistant.google.com/) (or any voice assistant that IFTTT supports)

## Media Playback Controls  - A Typical Use Case
Kodi 

```bash
sudo apt install kodi-eventclients-kodi-send
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

## Webhook - Listening and Responding to a Web Request

```bash
sudo apt install webhook
```

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
    ]
  }
]
````

start as a service
```bash
sudo systemctl start webhook
```

or auto-start as a service upon startup
```bash
sudo systemctl enable webhook
```

http://localipaddress:port/hooks/pictrl?action=play

## Port Forwarding - Exposing Local Service to the Public

Alternatively, Webhook Relay.

http://localipaddress
http://publicipaddress

## Dynamic DNS - Your Raspberry Pi's Permanent Domain Name

http://publicipaddress
http://domainname

## IFTTT - Connecting to A Voice Assistant

Link your Google account with
If this

then that
http://domainname:port/hooks/pictrl?action={{TextField}}

So now you will be able to use the following magic words to play (or pause) video on your Raspberry Pi.

```voice
Okay Google, Kodi play!
```

t

## Putting It All Together

The possibility is literally limitless.
