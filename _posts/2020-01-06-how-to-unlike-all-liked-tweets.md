---
layout: single
title:  "How to Unlike All Liked Tweets"
date:   2020-01-06 00:00:00 -0700
tags: [Twitter]
---

Happy New Year! So you want to delete everything you've ever liked on Twitter?

Open up your browser's developer console and paste this one-liner:

<!--more-->

```js
window.setInterval(() => { document.querySelectorAll('[data-testid="unlike"]').forEach(e => e.click()); window.scrollTo(0,document.body.scrollHeight); }, 2500);
```

Now, let it run until it's done.

What it does: It unlikes all tweets that have an unlike attribute set, then
scrolls the window to the bottom of the viewport, allows 2.5 seconds to load new
tweets and starts over again.
