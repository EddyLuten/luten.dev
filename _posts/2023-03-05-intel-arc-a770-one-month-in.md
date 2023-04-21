---
title: "Intel Arc A770: One Month In"
date:  2023-03-05 00:00:00 -0700
layout: single
tags: [Intel, Arc, Games]
twitter_image: /images/arc-box.jpg
---

![The Intel Arc A700 Box](/images/arc-box.jpg)

In building a PC mostly as a workstation, my choice of a GPU came as more of a secondary choice. My thought process was: sure, I'll play some games every once in a while, but really, this is my *work* machine. It needs to do workstation stuff and not much more.

<!--more-->

## The Buying Process

With that in mind, I put aside the thought of getting a beastly GPU like an RTX 4080 and looked at lower-end cards instead. My criteria: It had to be able to drive a 120hz 4k panel for desktop use, it had to fit in the ITX version of the Fractal Torrent, I wanted to be able to play Battlefield 2042 with my friends on Friday nights, and that's about it.

The obvious choice was an NVIDIA RTX 3060, which does all of the above at about $380-$400 retail. It's a good card and fits all of my criteria, but while researching, my eye fell on the newly released Intel Arc A770, which retails for $349 and shares similar performance characteristics.

The problem was that there were no Linux drivers available at the time, except for beta ones which were compatible with an older version of the kernel (5.17) with a promise of full compatibility in mid-February once kernel version 6.2 hit the streets. A bit of a gamble since my daily driver OS is Linux.

I've never been an early adopter of GPUs, and [pined for Larrabee](/larrabee) back in the day, so, I bought it and built the computer a month ago. What could possibly go wrong?

## First Impressions

On Windows 11, the card did what it was supposed to do: drive games and the desktop. I did experience a few hard crashes from time to time and am pretty sure they were caused by the GPU. Though, there were no error events in the Windows Event Viewer. Not quite a smooth experience, but really not that bad since I don't use Windows for anything serious.

On Linux, things were a bit rougher. Initially, I used whatever default driver Ubuntu came with, but it wasn't able to drive my panel at 120hz. For some reason, it was stuck at 80hz, max. That's not *that* bad, but the performance overall was quite poor. Noticeable lag while scrolling web pages and YouTube videos played with lots of screen tearing. So, I tried the beta drivers for Arc on Linux and downgraded the kernel to 5.17.

That worked smoother for a while until I ran `apt update` a few days later, which upgraded my kernel back to whatever the current version is.

A rough start on Linux, but the late-January drivers for Arc on Windows were usable enough.

## Latest Drivers

Things were bad on Linux, to say the least. On top of the issues mentioned before, attempting a screen-sharing session in Discord would crash several processes and send my system's fans into overdrive. I was beginning to regret being an early adopter since the OS I used to work with was being hamstrung.

However, once I upgraded to the shiny new Linux kernel 6.2, all my issues were resolved. My panel now runs smoothly at 120hz, I'm able to share my screen, and the system feels very snappy. Since I don't play games on Linux, I can't speak to the 3D performance, but as a workstation card, it does its thing and I am satisfied with it.

Crashes on Windows stopped for the games that I play once I upgraded to the latest February drivers. Before, [Satisfactory](https://www.satisfactorygame.com/) would occasionally dump to the desktop for no reason, but I have not experienced any issues with these new drivers.

## Conclusion

Would I recommend this card to hardcore gamers? No. Why take chances with brand-new technology when you rely on the GPU to work well *all* of the time?

Would I recommend this card to occasional gamers who mostly perform work on their machines? Definitely. You get the performance of an RTX 3060 at a lower average retail price. Just make sure that the games that you want to play perform well and don't have known issues.

I think Intel is off to a good start with their first generation of discrete GPUs and I look forward to their future releases.
