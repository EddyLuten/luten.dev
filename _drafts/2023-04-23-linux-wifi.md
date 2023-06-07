---
title: Monitoring WiFi Signal Strength on Linux
date:  2023-04-23 00:00:00 -0700
layout: single
tags: [Linux, WiFi]
---

Steps:

- `iwconfig` to find the interface name
- `watch -n 0.5 iwconfig <interface>`
- Move antennae until the signal improves

Still pretty bad quality in the same room as the router.

Will different antennae help?
