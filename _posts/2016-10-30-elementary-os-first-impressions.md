---
layout: single
title:  "Elementary OS First Impressions"
date:   2016-10-30 00:00:00 -0700
---

![elementary OS](/images/elementary-1.png)

It's been about a week of using elementary OS and I've compiled a few of my first impressions. First off, I want to start off with that I understand that elementary is still somewhat immature, so don't take any of the criticism as me putting the project on blast. Far from it, in fact, but more on that later.

<!--more-->

Installing elementary OS was a breeze. It's about as simple as installing macOS from a USB dongle. All my Intel NUC's onboard hardware was properly detected, HDD partitioning was not an issue and all happened automatically, and there was an option to enable encryption wherever it was applicable. Great process overall.

Boot times out of the box are snappy, it takes only a few seconds to go from POST to the OS itself. When you're presented with the desktop, it all looks really nice and sleek, but a bit derivative. It does look like it's emulating macOS, but that's not necessarily a bad thing. It has a different design aesthetic than macOS when it comes to icon design and where it places UI elements, but overall, it feels like a macOS clone.

![elementary OS screenshot](/images/elementary-2.png)

And that's where most of my issues that I have with the UX come from. Since it looks so much like macOS, you kind of expect it to behave like macOS as well and have the same features. Now I know that's not a fair expectation, but it's just the feeling I get when using it. Some features were copied, like hitting ⌘+Space for the Spotlight menu, called *App Launcher* or *Applications* in elementary, but doesn't offer much of the same functionality other than searching for applications or application features.

![elementary OS screenshot](/images/elementary-3.png)

One of these things that I feel is missing, for example, is the ability to change your screen's refresh rate, which has to be done through a system command, executed on every boot instead of through a drop-down menu. It kind of sucks since the frequencies listed aren't actually the parameters you use for the application, see this screenshot:

![elementary OS screenshot](/images/elementary-4.png)

Coming from macOS, I am very used to the keyboard shortcuts for Mac, so hitting ⌘-based commands is something I do all of the time. It doesn't help that I use a Mac at work and have to switch my muscle memory every night when I come home. I *could* remap all of the keys, but I feel like that's kind of missing the point of moving to a new OS. For now I'll just deal, even if that means opening up a Terminal window every time I want to open a new browser tab (⌘+T).

Third party software can be a bit of a hassle to install, such as Google Chrome if you're not used to installing downloaded packages with dpgk via the Terminal, but once it's installed, it's done. I do wish there was some kind of GUI-based installer for some of the `.deb` packages downloaded, though. Spotify in particular was a mess to install with missing dependencies not automatically resolving and, once it was installed, missing an option to minimize the player window.

Speaking of other things not working, I could not get my Bose QC35's working as an audio device. I was able to pair with it and read some of the workarounds online, but none of them seemed to work for me. If you got yours to work, I'd love to hear about it since I'm stuck using wired headphones via my monitor right now. **Edit:** got them to work simply via using the Bose Connect app on my iPhone and the elementary Bluetooth pairing app. Not sure what I did differently, but it all works great now.

Overall, the elementary OS experience has been good out of the box. I didn't have to make many adjustments to my development toolchain since most of the tools on macOS simply work the same on Linux. I didn't even switch out my `.bashrc` file, which is one of the first things I do on my Mac installs. The one that comes with the OS is decent to build upon.

Here's a list of stuff I'd like to see in future releases or through third-party software:

* The ability to move the dock to the left or right side of the screen
* Resizable dock icons, not just *large* or *normal* settings
* The ability to select my refresh rate via the system settings dialog
* The ability to install `.deb` files via the file explorer instead of the Terminal
* A system information screen that shows more than high level system details
* Some kind of task manager where I can monitor system resource usage and kill processes
* A proper replacement for Divvy, which I use extensively on the Mac

I may take a stab at some of these things since I don't see myself moving away from elementary OS anytime soon.
