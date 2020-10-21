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

Okay Google, pause Kodi.

<div align="center">
  <img src="https://shawenyao.github.io/Photos/IFTTT/logo.png" />
</div>

> “Any sufficiently advanced technology is indistinguishable from magic.”
> ― Arthur C. Clarke, Profiles of the Future: An Inquiry into the Limits of the Possible

Ever since Raspberry Pi came into my world, I have been exploring better ways to interact with it. Take Kodi the media player for example - yes, keyboard and mouse are fine; yes, its native web interface is super powerful; and yes, you can even use your TV remote directly if it's HDMI-CEC-compatible. But there's something about Raspberry Pi's small form factor (as well as its open source nature perhaps) that just makes me wish for a hands-free experience. 

To my surprise, there doesn't seem to be a satisfactory end-to-end tutorial anywhere that suits my need. However, that's about to change - please join me in my quest to build a voice-controlled Raspberry Pi. Before we dive into the technical mumbo jumbo, here is a list of all the hardware/sofware that we will need:
* [Raspberry Pi](https://www.raspberrypi.org/) and [Kodi](https://kodi.tv/)
* [Webhook](https://github.com/adnanh/webhook)
* [Port Forwarding](https://en.wikipedia.org/wiki/Port_forwarding)
* [FreeDNS](https://freedns.afraid.org/dynamic/)
* [IFTTT](https://ifttt.com/)
* [Google Assistant](https://assistant.google.com/) (or any voice assistant that IFTTT supports for that matter)

Okay Google, pause Kodi and let's get started.

## Media Playback Controls - A Typical Use Case
For those who are unfamiliar, Kodi is an all-in-one media center. For starter, it integrates almost every video streaming service on earth into a unified interface, be it YouTube, Netflix or even Google Drive. In addition to its core functionalities as a media player, Kodi supports extensions that can do much more through the installation of add-ons. Did I mention that it has a lovely weather widget, too? 

Kodi also shines in the controls department. On top of the keyboard/mouse, web interface or TV remote option, the ```kodi-send``` command lets the user control the player in command line. For example, if we are interested in replicating pressing the play button, we only need to create the following script ```/usr/local/bin/pictrl```

```sh
#!/bin/sh
action=$1

if [ "$action" = "play" ] || [ "$action" = "pause" ]
then
  kodi-send --action="PlayerControl(play)"
fi
```

and it's ready to roll. Since play and pause are basically the same command in different contexts, we also get the pause function for free.

**Milestone**: now your can use ```pictrl play``` in the command line interface (or over SSH) to play/pasue the video on your Raspberry Pi.

## Webhook - Listening and Responding to a Web Request

Next up we are going to trigger that ```pictrl``` script with an http request. For that, we need webhook, a cool piece of technology that enables responding to http requests with custom callbacks. 

To start using webhook, first create the configuration file ```/etc/webhook.conf```:
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

that points a new webhook instance to the ```pictrl``` command. After that, the webhook can be started as a service using:
```bash
sudo systemctl start webhook
```

or auto-started upon startup by running:
```bash
sudo systemctl enable webhook
```

Note that for such a service that is intended to be accessible over the internet (as will become true in the next step), it's probably a good idea to authenticate the identity of the requestor in some form. For example, you can ask the requestor to submit a token that only a trusted user knows along with the request itself.

**Milestone**: now your can use the link ```http://localipaddress:port/hooks/pictrl?action=play``` on any device within the same network to control your Kodi player.

## Port Forwarding - Exposing Local Service to the Public

A local IP address, obviously, isn't visible outside the local network. To fix the problem, it's usually necessary to log on to your modem/router as admin and configure what's known as a port forwarding. From then on, instead of using ```http://localipaddress:port``` locally, we can call ```http://publicipaddress:port``` over the internet and the request will be directed to the same place.

In case you don't have admin control over your modem (which is unfortunately true in my case), [Webhook Relay](https://webhookrelay.com/) can be helpful although its free tier only supports up to 150 "relays" per month.

**Milestone**: now your can use the link ```http://publicipaddress:port/hooks/pictrl?action=play``` on any device on the internet to control your video player.

## Dynamic DNS - Your Raspberry Pi's Permanent Domain Name

For most home internet users, chances are that tier public IP addresses aren't static. With each reboot of the modem, a new IP address will be assigned which makes it annoying when you are looking for a more permanent solution. Don't worry - dynamic DNS services such as FreeDNS can come to the rescue. These services essentially maintain a list that maps domain (or subdomain) names to IP addresses, and each user tells them to update the list whenever the IP address changes. To do this, run the following command at Raspberry Pi's startup:
```bash
wget https://freedns.afraid.org/dynamic/update.php?[yourtokenhere]
```

If all goes well, instead of changing ```http://publicipaddress``` each time the modem restarts, a new and permanent name ```http://domainname``` is all we have to remember.

**Milestone**: now your can use the link ```http://domainname:port/hooks/pictrl?action=play``` on any device on the internet to control your video player.

## IFTTT - Connecting to A Voice Assistant

IFTTT, short for "If This Then That", provides a convenient way to create a hub that connects a variety of services (including voice assistants) where they can interact with each another based on a set of user-defined rules (called applets). As of the time of writing, IFTTT allows each user to create up to 3 applets for its free tier.

As the name implies, every applet of IFTTT follows the "If This Then That" structure:

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/1.jpg" />
</div>

and creating a new applet boils down to defining the two pieces: "If This" and "Then That". First, configure the "If This" part and choose the Google Assistant option (you might be asked to link your Google account to IFTTT). In the next screen, although the "Say a simple phrase" option is more than enough to get the job done, the "Say a phrase with a text ingredient" option is preferred as it will be a lot more flexible when it comes to further customizing our voice commands.

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/3.jpg" />
</div>

That brings us to the trigger configuration. I use "kodi" as my keyword, followed by a custom text field. The rest is not important.

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/4.jpg" />
</div>

Next, on the "Then That" piece, what we want to choose is the webhook service that we've created in the previous step, with the exact action being configurable for future development's sake:

<div align="center">
  <img width="50%" height="50%" src="https://shawenyao.github.io/Photos/IFTTT/6.jpg" />
</div>

Save and continue. That's it - our first IFTTT applet has just become fully operational.

**Final milestone**: now you can say the following magic words to play (or pause) your video on your Raspberry Pi's Kodi player:

```bash
Okay Google, Kodi play!
```

## Putting It All Together

<div align="center">
  <img src="https://shawenyao.github.io/Photos/IFTTT/logo2.png" />
</div>

As you might have noticed by now, your voice can literally be as powerful as your computer is. The toolchain we've established so far makes it possible to invoke almost any action of our choice with almost any words of our choice. The best part is, all the extra development work will only need to happen locally inside the ```pictrl``` script. That said, what to do with such limitless possibility might be a matter of user experience at the end of the day, so please let me know what your mileage turns out to be.

## Appendix
### Install all the software needed on the Raspberry Pi
```bash
sudo apt install kodi
sudo apt install kodi-eventclients-kodi-send
sudo apt install webhook
```
