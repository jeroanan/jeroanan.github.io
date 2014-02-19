---
layout: post
title:  "Wireless Problems"
date:   2014-02-19 20:30:00
categories: problems
---

For several days I was experiencing wireless problems with Linux Mint 15. I'd either have a connection that'd quietly stop working after a while (without appearing to have disconnected), or on power-on, my computer would repeatedly ask me to authenticate the wireless and not connect at all. A look at dmesg would give me something along the lines of the following:

wlan0: deauthenticated (Reason: 15)

Google wasn't much help. Clearly the four-way handshake made during authentication was timing out, but there wasn't much in the way of how to fix it. So what did I do? I updgraded to Linux Mint 16. That was four days ago, and I've not seen the problem since.