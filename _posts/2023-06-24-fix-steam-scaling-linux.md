---
title: Scaling Issues on Linux Workaround
date:  2023-06-24 00:00:00 -0500
layout: single
tags: [Steam, Games]
twitter_image: /images/steam-big.png
---

![Steam Scaling](/images/steam-big.png)

If you're on Linux and received the latest Steam patch that makes your UI scaling look overly large, here's a quick workaround until Valve fixes the application (and given that you have a Steam desktop shortcut).

Open up the Steam desktop launcher shortcut (`~/Desktop/steam.desktop`) in your favorite text editor and find the line that starts with `Exec=`. You'll want to change it to the following:

```txt
Exec=/usr/bin/steam -forcedesktopscaling 1.0%U
```

You can change the scaling factor to something other than 1.0, but that's the value that worked for me without breaking the entire UI. The only downside is that you'll have to launch Steam from this desktop shortcut until Valve fixes this.
