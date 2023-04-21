---
title: Five Quick Check-In Guidelines
date:  2011-01-17 00:00:00 -0700
layout: single
tags: [Programming]
---

If you work in a source controlled environment, these are the minimal guidelines that you'll have to stick to for making your teammates' lives a bit easier.

1. **Don't Check-In Broken Code**: More than often, you'll pull down the latest version of a project from your repository only to find that the code won't build. Please, don't check-in code to the main project that doesn't compile, even if you intend to pick up the slack the next day. However:
1. **Don't Go Home Without a Check-In**: Even though you shouldn't check-in your broken code to the main branch, many source control systems have a way to branch a user's changes and merge them back later. If you're using Team Foundation Server, take a look at Shelve Sets.
1. **Use Check-In Comments**: Always leave a descriptive comment of the work you've done when your check-in. Your teammates weren't hired to analyze undocumented code, so that 500-line change across multiple files better have a comment.
1. **Check-In Association**: If your source control system allows this type of integration, associate your check-in with a work item, bug, or help-desk ticket. If it does not, at least make a reference to the work item's identifier in the comment section.
1. **Use Check-In Policies**: Use check-in policies to ensure that all of the above things aren't impeding your build if your source control system supports them. These policies make your life easier and disallow sneaky developers from checking-in their broken spaghetti code.

Share any tips you may have!
