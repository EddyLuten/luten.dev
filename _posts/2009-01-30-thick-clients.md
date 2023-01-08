---
title: Thick clients? Gimme a break.
date:  2009-01-30 00:00:00 -0700
layout: single
---

Neil McAllister of InfoWorld recently made his [case against web-based applications](https://web.archive.org/web/20090206202204/http://weblog.infoworld.com/fatalexception/archives/2009/01/the_case_agains.html). He gives five reasons for companies not to use web based technologies.

Having developed for both platforms (desktop and web) professionally, I can say with all certainty that Neil McAllister is wrong in his assertions.

Web applications try to mimic the realtime behavior of desktop applications, there's no doubt about it. But the one thing that's to think about is: Would a desktop application scale in the 21th century?

What I mean by this is: Would I be able to use my desktop application on Mac, Linux and Windows at the same time? With the exception of Java apps, the answer is a resounding "no".

Desktop applications don't do so well when they have to be ported to multiple platforms since they have to be recompiled on the targeted platform. In addition, if you have offices overseas or people working from their homes, thick clients don't make sense.

I think when Neil was halfway through his post, he must have doubted his writing since the article mentions using "consistent UI Toolkits" like the Win32 API, Cocoa etc. Now, anyone who's worked with desktop applications knows that UI design for the desktop is moving heavily towards an XML/style based approach, influenced by the web (WPF, etc.).

All of the APIs mentioned are not cross platform compatible so a cross platform abstraction layer has to be put in place with all its limitations for the application to be able to run. If you've read the last two paragraphs, you've probably already figured out that creating an application that would scale on the same amount of platforms as a web application would be extremely costly and time consuming.

As for cross browser compatibility, it's not that big of a deal as it was in the early years. All of the quirks that cross browser development brings are known to (proficient) web designers and developers and are taken into consideration when designing a User Interface.

As for online access by employees, invest in an internet filter with the money you save going from desktop development to web development and you're all set. But really, if your employees access porn websites at work, there's something really wrong with your hiring process and the motivation levels at your company.

Good luck trying to get these damn interweb kids off your lawn.
