---
title: "Hungarian Notation: What to do?"
date:  2009-01-21 00:00:00 -0700
layout: single
tags: [Programming]
---

Edit: FYI, by Hungarian notation, I mean Systems Hungarian such as bIsSucky.

It seems I’m in some kind of pickle. For some reason, two of the programmers at the company I work for still use [Hungarian notation](https://web.archive.org/web/20090206202204/http://en.wikipedia.org/wiki/Hungarian_notation).

In case you don’t know what that is, in short: Hungarian notation prefixes an abbreviation of either the data type or purpose of the variable to its name. For example, Microsoft’s WINAPI still uses it, hence we have things such as hInstance, nShow, szCompany, etc. So it’s quite ugly and confusing to the programmer.

Yet these two programmers still cling to their old ways and refuse to give up on this ancient method. Even in VB.NET. One of these programmers happens to be Joe the Programmer mentioned before, go figure.

I was asked by one of them “Why not use Hungarian notation?” In case you dind’t know, dear reader, the name of the variable should give away the data type, use UpperCamelCase and logic for your naming conventions. Turns out, UpperCamelCase is a programming convention in this company, so why we were arguing, I don’t know. Now if only logic were a convention, we’d be set.

But it was like pissing against the wind as neither them nor I were persuaded in the end. How would you persuade a person to switch to a different methodology? By them using Hungarian notation, people who will eventually take over their source code will want to shoot themselves.
