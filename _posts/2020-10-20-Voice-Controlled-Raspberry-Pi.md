---
layout: post
title: Voice-Controlled Raspberry Pi
tag:
  - raspberry pi
  - voice assistant
  - smart home
comments: true
draft: true
berry: true
new: true
---

Yet another tutorial.

> “Any sufficiently advanced technology is indistinguishable from magic.”
> ― Arthur C. Clarke, Profiles of the Future: An Inquiry into the Limits of the Possible

Before we start, here is a list of all the hardwares/sofwares that we will be using.
* [Raspberry Pi](https://www.raspberrypi.org/) and [Kodi](https://kodi.tv/)
* [Webhook](https://github.com/adnanh/webhook)
* [Port Forwarding](https://en.wikipedia.org/wiki/Port_forwarding) or [Webhook Relay](https://webhookrelay.com/)
* [FreeDNS](https://freedns.afraid.org/dynamic/)
* [IFTTT](https://ifttt.com/)
* [Google Assistant](https://assistant.google.com/) (or any voice assistant that IFTTT supports)

## Media Playback Controls  - A Typical Use Case
Kodi 

```/usr/local/bin/pictrl```
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

Webook is a cool piece of technology that enables resonding to http requests with custom callbacks. 

To start using webhook, first create the configuration file ```/etc/webhook.conf``` that points a webhook id to the ```pictrl``` command:
```json
[
  {
    "id": "pictrl",
    "execute-command": "/usr/local/bin/pictrl",
    "command-working-directory": "/home/pi/",
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

After that, the webhook can be started as a service using
```bash
sudo systemctl start webhook
```

or can be auto-started upon startup by running:
```bash
sudo systemctl enable webhook
```

Note that for such a service that will be accessible over the internet (as it will be the next step), it's probably a good idea to authenticate the identity of the requestor in some form. For example, you can ask the requestor to provide a token that only a trusted user knows along with the request itself.

**Milestone**: now your can use the link ```http://localipaddress:port/hooks/pictrl?action=play``` on any device within the same network to control your Kodi player.

## Port Forwarding - Exposing Local Service to the Public

Alternatively, Webhook Relay.

http://localipaddress
http://publicipaddress

**Milestone**: now your can use the link ```http://publicipaddress:port/hooks/pictrl?action=play``` on any device on the internet to control your video player.

## Dynamic DNS - Your Raspberry Pi's Permanent Domain Name

http://publicipaddress
http://domainname

**Milestone**: now your can use the link ```http://domainname:port/hooks/pictrl?action=play``` on any device on the Internet to control your video player.

## IFTTT - Connecting to A Voice Assistant

IFTTT, short for "If This Then That", provides a convenient way to create a hub that connects a variety of services (including voice assistants) where they can interact with each another based on a set of used-defined rules.

First, let's create a new applet. As the name implies, every applet on IFTTT follows the "If This Then That" structure:

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/1.jpg" />
</div>

Next, configure the "If This" part and choose the Google Assistant option. You might be asked to link your Google account to IFTTT.

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/2.jpg" />
</div>

Although the "Say a simple phrase" option is more than enough to get our job done, the "Say a phrase with a text ingredient" option will be a lot more flexible in terms of further customizing our voice commands.

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/3.jpg" />
</div>

That brings us to the trigger configuration. I use "kodi" as my keyword, followed by a custom text field. The rest is not important.

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/4.jpg" />
</div>

On the "Then That" piece, what we want to choose is the webhook service

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/5.jpg" />
</div>

that we've created in the previous steps, with the exact action being configurable for future expansion:

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/6.jpg" />
</div>

There we go - our first IFTTT applet has become fully operational.

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/7.jpg" />
</div>

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
