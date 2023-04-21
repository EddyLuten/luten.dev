---
layout: single
title:  "PortAudio Panic and No Devices Found"
date:   2017-02-14 00:00:00 -0700
tags: [Linux]
---

Leaving this here for the poor souls on Linux systems that run into errors accessing the default input or output devices using PortAudio and get nothing back.

<!--more-->

Maybe you're using rust-portaudio and your application panics after accessing `default_output_device` or `default_intput_device` even though you clearly have default audio devices set:

> thread 'main' panicked at 'called \`Option::unwrap()\` on a \`None\` value'

This pretty much means that you don't have libasound installed on your system. While the PortAudio project [mentions this](http://portaudio.com/docs/v19-doxydocs/compile_linux.html) in its build documentation, the Rust version of this library doesn't explicitly mention this dependency.

On Debian-based systems (Ubuntu and whathaveye), run the following command to cure this:

```bash
sudo apt-get install libasound2 libasound2-dev
```
