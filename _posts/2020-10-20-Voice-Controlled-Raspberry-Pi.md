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

/usr/local/bin/pictrl
```sh
#!/bin/sh
action=$1

if [ "$action" = "play" ]
then
  kodi-send --action="PlayerControl(play)"
fi
```

**Milestone**: now your can use ```pictrl play``` in the command line interface (or over SSH) to play/pasue the video on your Raspberry Pi.

## Webhook - Listening and Responding to a Web Request



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

**Milestone**: now your can use the link ```http://localipaddress:port/hooks/pictrl?action=play``` on any device within the same network to control your Kodi player.

## Port Forwarding - Exposing Local Service to the Public

Alternatively, Webhook Relay.

http://localipaddress
http://publicipaddress

**Milestone**: now your can use the link ```http://publicipaddress:port/hooks/pictrl?action=play``` on any device on the Internet to control your video player.

## Dynamic DNS - Your Raspberry Pi's Permanent Domain Name

http://publicipaddress
http://domainname

**Milestone**: now your can use the link ```http://domainname:port/hooks/pictrl?action=play``` on any device on the Internet to control your video player.

## IFTTT - Connecting to A Voice Assistant

Link your Google account with
If this

then that
http://domainname:port/hooks/pictrl?action={{TextField}}

**Milestone**: now you can say the following magic words to play (or pause) your video on your Raspberry Pi's Kodi player:

```bash
Okay Google, Kodi play!
```

## Putting It All Together

The possibility is literally limitless.

## Appendix
### Install all the softwares needed
```bash
sudo apt install kodi
sudo apt install kodi-eventclients-kodi-send
sudo apt install webhook
```
