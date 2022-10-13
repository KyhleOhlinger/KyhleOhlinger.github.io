---
title: Blocking Ads within my Home Network
author: kyhle
date: 2022-10-13 12:00:00 +0200
categories: [InfoSec, Technical]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/pi.png
  width: 800
  height: 150
---

Over the weekend I was bored and decided to undertake a small project of removing ads from my home network. Initially, I looked into [CloudFlare Zero Trust](https://www.cloudflare.com/products/zero-trust/) which is free and runs on a serverless architecture. Marco Lancini has a great [blog post](https://blog.marcolancini.it/2022/blog-serverless-ad-blocking-with-cloudflare-gateway/) on it if you're interested. 

I went through the process and installed it on my PC and cellphone, the main benefit here was that I could connect to any network with the VPN enabled and have my adblocking lists with me wherever I went. The major downside is that each client that connects to the network will require a CloudFlare root CA, in addition to the WARP client. After setting it up, this method did not seem reasonable as I have several devices and I wanted it to be enabled for my entire network and for whoever joins my home network at any point (friends, family, the neighbourhood squirrel, etc.). 

### What is a Pi-Hole?

In Marco's blog, he mentioned the similarities between CloudFlare Zero Trust and [Pi-hole](https://pi-hole.net/) (a Raspberry Pi based network wide ad blocker). Fortunately for me, my partner had a spare Raspberry Pi lying around which I used to create a Pi-Hole. This had the advantage of providing network wide ad filtering, but it would require capital expenditure to purchase the Raspberry Pi if you don't have one readily available.

To get it up and running, you need to install the software to a Raspberry Pi running Raspberry Pi OS, run an installation script, and direct your network traffic to the Raspberry Pi's IP address. If you would like to set this up at home, you will need:

- A Raspberry Pi with an Ethernet port
- Power and Ethernet cable for your Raspberry Pi
- A PC, I found it easier with Linux, but Windows or Mac will also work


### Setting up a Pi-Hole

This post isn't a tutorial on how to install it, if you want to install this on your network, I do recommend following [this](https://www.tomshardware.com/how-to/set-up-pi-hole-raspberry-pi) guide, but I have included the basic steps below:

- Download and install Raspberry Pi Imager from the Raspberry Pi website.
- Insert a microSD card into your computer.
- Launch Raspberry Pi Imager and open the advanced configuration menu.
- Enable SSH and then set a new SSH password.
- Select the OS that you want to use, I went with Raspberry Pi OS (32-bit). 
- Write the OS to your microSD card and insert the card into your Raspberry Pi.
- Connect your Raspberry Pi to the network via an Ethernet cable.
- Connect to the Raspberry Pi using SSH - If you want to determine the IP address, I went into the router and looked for the Raspberry Pi under network connections
- Update your software repositories and then download the latest updates for your Raspberry Pi using the following commands:

```bash
sudo apt update
sudo apt upgrade -y
```
- Install Pi-hole using the following cURL command:

```bash
curl -sSL https://install.pi-hole.net | bash
```

- Follow the prompts and you will now have a functioning Pi-Hole
- Once it is up and running, set your router's primary DNS to the Pi-Hole's IP address to ensure that all network traffic is going through the device.
- Access your web interface on <http://IP-ADDRESS/admin>.

With everything configured, your network traffic should be redirected to Pi-hole's DNS servers which can block unwanted advertisements. You may find that some of the sites that you normally access are blocked. Don't worry, the same [guide](https://www.tomshardware.com/how-to/set-up-pi-hole-raspberry-pi) contains a section on Allowing traffic to those sites by adding them to an allowlist. I also highly recommend adding the Regex filters described in this [Youtube](https://www.youtube.com/watch?v=o-bxDuH_T6I) video to the blocklist.

### Why Bother?

My main use case was removing ads from my YouTube mobile app which, unfortunately, was not possible because, as discussed in the [subreddit](https://www.reddit.com/r/pihole/comments/vd2agc/blocking_youtube_ads/), Pi-hole blocks based on DNS resolution and that YouTube hosts their own ads under the YouTube domain which means that Pi-hole is not really effective in this case.

However, after installing it, it did improve my browsing drastically. My top use-cases for Pi-Hole are:
1. Removing ads from various applications/sites across multiple devices.
2. I find that the Pi-Hole serves as a decent network monitor, but this will depend on your router as described [here](https://discourse.pi-hole.net/t/why-do-i-only-see-my-routers-ip-address-instead-of-individual-devices-in-the-top-clients-section-and-query-log/3653).
3. Automatically dealing with Apple Private Relay and Firefox's DNS-over-HTTPS (DoH).

Additional use-cases:
- Extra bandwidth that comes with blocking upwards of 20% of your network traffic.
- Removing cross-platform tracking.
- Ability to deny access to various platforms that you spend too much time on, e.g. *.twitter.com, *.facebook.com, etc.
- Take it with you on the road - you can connect to other networks and set the Pi-Hole DHCP- and DNS-Server.
- PiVPN allows you to VPN to your home network, however this will have the same negatives as described above regarding CloudFlare.

If you have a method to reliably block YouTube mobile ads, please do reach out to me as I'd love to hear about it. Also, if you have any additional questions, please reach out! I hope that you found this interesting and at the very least, learned about an additional benefit of using a network based adblocker.