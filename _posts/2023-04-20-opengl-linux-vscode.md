---
title: OpenGL in C# on Linux using Visual Studio Code
date:  2023-04-20 00:00:00 -0700
layout: single
tags: [OpenGL, Linux, C-Sharp, '.NET', VSCode]
---

I've been out of the .NET loop for a *very* long time. I would never have thought that it was so easy to get a .NET project up and running on Linux. But, I guess a decade of embracing Open Source at Microsoft changes things. Here are the steps I took to get an OpenGL window up and running on Ubuntu using .NET Core, VSCode, and OpenTK.

<!--more-->

Open up the command line and create a directory for your project, then `cd` into it.

Register the apt repositories listed on [this website](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu#register-the-microsoft-package-repository).

Install .NET Core:

```zsh
sudo apt install dotnet-runtime-7.0 dotnet-sdk-7.0
```

Once installed, set up a solution:

```zsh
dotnet new sln
```

Followed by the main executable project:

```zsh
dotnet new console -o game --use-program-main
```

I named the project `game`, but call it whatever you want. While still in the solution directory, add the new project to the solution:

```zsh
dotnet sln add game
```

Now `cd` into the game directory and add the OpenTK package:

```zsh
dotnet add package OpenTK
```

*That's it.* Follow the tutorial at [The OpenTK site](https://opentk.net/learn/chapter1/1-creating-a-window.html?tabs=baseclass-opentk3%2Cgamewindow-ctor-opentk3%2Cgamewindow-run-opentk3%2Ckeypress-opentk3), and you should be up and running. If you install the official [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp), you should be able to use the same keybindings from Visual Studio to run and debug your program.

I can't think of an easier way to create a cross-platform OpenGL executable than this. This setup is great for little demos and trivial graphical apps that don't need to be blazing fast. Not to mention being able to do your primary development cycles in Linux, with its dev-centric *nixy tools, and switching to Windows once the program is completed and ready for distribution. It's a far cry from the burning hoops I had to jump through a decade ago with Mono and a lack of tools outside of Windows.
