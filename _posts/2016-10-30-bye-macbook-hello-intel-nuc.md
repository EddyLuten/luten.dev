---
layout: single
title:  "Bye MacBook, Hello Intel NUC"
date:   2016-10-30 00:00:01 -0700
tags: [Intel, Apple]
---

For a while now, my 2011 13" i5 MacBook Air which I use for development purposes has been showing signs of pending death: flickering screen when moving the lid, excessive heat, inability to be charged, killing 2 replacement batteries and 3 chargers, slowing down with new OS X/macOS installs, etc. etc.

<!--more-->

So, I figured that it was time for a new machine. The MacBook Air, whose form factor I love, served me well (not counting the recent death rattles) for 5 years, so I eagerly awaited the October 27 Mac event, eyeing either a replacement MacBook Air or a new iMac. In short, this is what happened:

* No new iMacs, Mac Mini, NOR MacBook Air models.
* Removal of ports that I use *all the time* on my MacBook.
* An uninspired hardware refresh.
* Entry level MBP is $1,499?! And no Touch Bar. I mean, I didn't want one, but I think that it should have one for 1.5k.

There are many more threads on Reddit and a ton of other sites that lament the event, so I won't dedicate more space to it except that I bought a 15" i7 MacBook Pro with 16GB of RAM and NVIDIA GPU in 2012 for only $300 more than the cost of the current entry level MPB. Needless to say, I won't be continuing my usage of Apple hardware.

## So What Are My Choices?

My initial reaction was to either dual boot my gaming machine into macOS by turning it into a Hackintosh. Something I had done before, which worked *okay*. The main issue is that my gaming machine is also from the stone age of 2011 and carries around an i7 2600k running on a P67 motherboard. This works fine for gaming, but not so much for the Clover bootloader.

My second idea was to build a tiny i3 6100 based machine using a HTPC form factor case. And I had it all specced out, costing about $390 in total. But then I came across a mention about Intel NUC while watching an HTPC case review. I was surprised that I never heard of it before.

## Enter NUC

Intel NUC is a PC sans RAM, storage (and, thus, OS) for as little money as you could put together an HTPC yourself. I went to the Intel site, saw a version of it with an i3 6100U (NUC6i3SYH), found it on Amazon for $277.60 and smashed the buy button.

![Height](/images/nuc.jpg)

I had an unused SSD laying around, a Samsung Evo 850 250GB, and ordered some cheap-ish DDR4 RAM from Crucial, 16GB in total. The total cost for all the hardware, without shipping and taxes was $347.59. I had that SSD laying around, so if you wanted one with an Evo 850 like mine, add about $99.99 to that number.

So what's better than building one from scratch? Features. The motherboard you get in a MicroATX machine at that price point does not support Bluetooth, WiFi, mini-DisplayPort connectivity, VESA mountability, SD card reader, and has a much worse form-factor to accommodate the power supply and fans.

The height of the NUC is about the same as 5 CD jewel cases stacked on top of eachother at about 53mm, but with a smaller surface area. You couldn't put an optical drive in one of these simply because a disc is larger than the width + height of this thing.

![CD](/images/nuc2.jpg)

As I mentioned above, it comes with a VESA mounting bracket so you could attach the whole kit and caboodle to the back of your screen for the most minimal footprint possible and to get that all-in-one feel. Sadly, my monitor's stand is attached to the VESA mount, so it's not possible for me. However, I will probably Jerry-rig something together to get it off my desk.

Putting the hardware together was incredibly easy. Four screws holds a plate exposing the internals. This model comes with a cradle for a 2.5" HDD, which you can just slide in without worrying about screws or cables. You slip it in and you're done. Adding RAM is the same procedure as adding RAM to a laptop, a simple process of lining up the notches and pushing them into the slots. It took less than 5 minutes to unscrew, pop in the SSD, pop in the RAM, and screw it back together. Easiest. Assembly. Ever.

![Guts](/images/nuc3.jpg)

## What's Next?

I'm installing elementary OS onto it instead of macOS. Actually, I already have and am typing this from elementary OS. The system feels fast and responsive, which I didn't expect from an i3 processor and an integrated graphics chip driving a 2560x1440 screen at 144hz. Supposedly, the NUC is compatible with Hackintosh builds, but I wanted to try something new first and it's been a while since I've used Linux on the desktop. If it doesn't work out, I'll attempt a Hackintosh build later on. For now, I am impressed with my sub-$350 PC and I'll write a post with my elementary OS impressions after I've used it for a bit.
