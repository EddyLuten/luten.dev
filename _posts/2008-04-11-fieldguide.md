---
title: Direct3D, OpenGL and XNA Fieldguide
date:  2008-04-11 00:00:00 -0700
layout: single
---

A common novice's question in context with graphics programming is which API should I use?, Direct3D versus OpenGL or which API is better?. Getting familiar in the Graphics Programming world can be tough since many subjects don't have definitive answers. This article attempts to clear up some of the mysteries surrounding the APIs and compare them as far as it is possible. The individual APIs discussed in this document are Direct3D, OpenGL and XNA. If you're new to Graphics Programming in general, read the Graphics Programming article to get a clear understanding of what exactly these APIs do.

This article is not intended to explicitly tell you which Graphics API to use, rather it simply explorer the features and limitations of the APIs discussed.

## About Graphics APIs

The following sections explain what a graphics API is, what it does and what influences a Graphics API. The points here are simplified to provide a basic understanding.

### A Graphics API is not

The following two section define what a Graphics API is not. If you're looking for the topics provided here, some suggestions are made for you to continue your search.

#### ...a Game Engine

To be clear about what's being discussed here: Direct3D, OpenGL and XNA are not game engines. A game engine is a library or program dedicated to delivering high performance interactive 3D graphics, sound, networking, etc. A Graphics API is simply a low-level mechanism to deliver visual content to a computer's screen. Some examples of game engines are Delta3D, NeoEngine and the C4 Game Engine.

#### ...a 3D Engine

While 3D Engines such as Ogre3D, Irrlicht, et al implement Graphics APIs, they usually provide access to higher-level functionality such as loading models, mathematical functionality and scene management. The graphics APIs don't provide such functionality but allow the user to create the functionality themselves through API functions provided.

### Graphics APIs Usage

After reading the previous section, you might wonder what a graphics API does since it doesn't create games or manage a scene. Think of a Graphics API as a way to talk to your graphics hardware. A Graphics API allows you to tell your hardware to draw a pixel at location X in a human understandable format.

The Difference between the APIs being the syntax of the way you talk to the hardware. To draw a pixel, API A might require you to type `DrawPixel(left, top);` while API B requires you to say `PutPixel(left, top);`. Another difference might be the way the API is initialized and made functional in the context of the code.

#### The Display Driver's Role

The display driver's role is to translate API and operating system functions into a hardware interpretable format. To understand how the process works, here's a simplified list with the steps involved from the program to the hardware:

* Program sends an instruction to the API
* API sends the instruction to the Display Driver
* Display Driver sends the instruction to the operating system
* The operating system sends the instruction to the CPU
* The CPU sends the instruction to the graphics hardware

Display drivers require to be updated every now and then. This is because the driver is the intermediary piece between the API and the hardware and is a piece of software, which like all software might contain bugs. Another reason for these updates might be because of added or updated functionality for a specific Graphics API.

Without the presence of a display driver or nonsupporting hardware, an API will likely fall back to a software implementation which means that all API routines will be executed by the CPU. This means that hardware acceleration will not be supported and the execution times are likely to be much higher.

#### API Image Quality

Contrary to popular belief, APIs rarely (if ever) affect the quality of the final image. To understand why, one must envision the different APIs talking to the same piece of hardware. When API A says `DrawPixel(x,y);` the hardware receives this as an instruction in machine code and executes this. When API B says `PutPixel(x,y);` the same instruction will be executed with the exact same machine code.

If a difference in image quality does exist, it is most likely due to the way the display driver interprets the command sent and transforms it into machine code for the graphics hardware to consume or because an API performs an automated transformation beyond the user's control.

When comparative images show up, it is best to avoid arguments and simply ignore the statements being made since APIs have no control over how the hardware display an image. The only factors in the image quality are the quality of the artwork, the ability of the hardware and the amount of hardware integration (the amount of hardware functions) the graphics API provides.

#### API Performance

While image quality barely plays a role when considering an API, different APIs can certainly have performance differences. This is usually because of the amount of abstraction occurs between the API and the hardware. Abstraction simply means the amount of functional layers between the API and the hardware. Performance leans heavily towards the amount of code that's being processed, so in many cases more code equals lower performance.

## Introduction to the APIs

### The OpenGL API

The OpenGL API is certainly the oldest graphics API between the three discussed in this article. Conceived in 1992 by Silicon Graphics as an open standard for graphics hardware instructions across multiple platforms, it has proven to withstand the test of time being virtually implemented on all major operating systems.

### The Direct3D API

The Direct3D API is a proprietary graphics interface for Microsoft platforms such as Microsoft Windows and the Xbox platforms. It was conceived in 1995 for the Windows 95 operating system as part of the Windows Game SDK, which was later renamed to DirectX. Direct3D currently handles all 3D and 2D instructions within the DirectX SDK.

### The XNA Framework

The XNA Framework is the youngest of the APIs discussed here, being released in 2007. XNA is an interface built on top of the DirectX SDK and provides high-level Object Oriented functionality for video games. XNA is currently only available in the C# programming language since it's a managed library based off the Microsoft .NET framework. XNA currently only works on the Microsoft Windows and Xbox 360 platforms.

## Comparing the APIs

### Cross-Platform Support

When a program will solely run on a single platform, the choice between APIs is usually fairly clear. But it is likely that a product, whether it be a video game or professional software, has to be supported on various platforms.

Currently, the OpenGL API is the only API supported on most major platforms including Microsoft Windows, various Linux distributions and Macintosh. The OpenGL API cannot be operated on the Xbox and Xbox 360 platforms, but can be used on the PlayStation 3 platform.

The Direct3D API will only run on Microsoft platforms such as the Xbox, Xbox 360 and Microsoft Windows but can be emulated on Linux platforms through Wine which reroutes Direct3D API calls to the OpenGL API.

The XNA Framework is currently only supported on Microsoft platforms that can run the .NET framework which is limited to Microsoft Windows XP, Windows Vista and the Xbox 360.

### Ease of Use

All three APIs are fairly simple to use with XNA being the simplest API and Direct3D being the most complex API in terms of code syntax. Since Direct3D and OpenGL are both native C libraries, the interface provided does not implement any classes or namespaces.

XNA on the other hand is strictly a .NET platform enabled Framework which means that it cannot be used by native languages, only by managed languages but implements classes and namespaces. XNA also includes a myriad of helper functions and libraries and is fully compatible with the .NET framework.

This means that while OpenGL and Direct3D both are closer to the hardware and can be ported to a higher level language, the time it takes to develop an OpenGL or Direct3D application will be higher than that of an XNA application. The trade-off is explained in the next section.

### Performance

Since OpenGL and Direct3D are C-based APIs, they are closer to the hardware and implement fewer levels of abstraction. This means that the performance differences between Direct3D and OpenGL are minimal. Any significant performance differences are likely to be the result of the way the display driver interprets the API commands.

The XNA Framework on the other hand is a .NET library which invokes native Direct3D calls to be used on the virtual machine in which the .NET Framework operates. This high level of abstraction can cause performance issues and it is recommended to use the XNA Framework solely for lower performance applications.

### Features

APIs are usually limited by the amount of features they implemented at the time of release. This causes the developers of the API to update the API, increase the version number and release a newer version. DirectX/Direct3D is limited by such restrictions, yet updated versions of the SDK are being release routinely every three months.

The OpenGL API includes an extension mechanism which allows independent hardware vendors or end-users to implement their own features whenever a driver is released or with a next generation of graphics cards.

The XNA Framework is based on Direct3D version 9 and can only include the functionality provided by this API. If a newer version of Direct3D is released, the XNA Framework will have to implement the new functionality afterwards. This causes the library to be one to several versions behind current standards.

### Support

The OpenGL API is a community supported and developed product and currently has a new version scheduled for 2008, OpenGL 3.0. The OpenGL API is not often updated, 2.1 being the latest version from 2006 and development has fallen behind schedule as OpenGL 3.0 was supposed to be released in 2007.

The DirectX API is both community supported and professionally supported. Professional support requires at least an MSDN subscription to access the support features. A new version of the DirectX API is released every three months.

The XNA Framework is also both community and professionally supported, similarly to DirectX. XNA releases are announced in advance but doesn't have a set update schedule.

### Popularity

The Direct3D API is extremely popular with Windows and Xbox platform developers where the gross of the game development occurs. Since Direct3D is developed by Microsoft, it lends itself well towards Microsoft's platforms.

The OpenGL is popular amongst both professional graphics developers and game developers, although its usage in video games has declined somewhat since the early 2000's. It is the only available option on non-Microsoft platforms for hardware accelerated graphics.

The XNA Framework is very popular with hobbyist programmers and lends itself well towards learning how the concepts of both 3D and 2D programming works. Yet, only a few professional titles have been released using the XNA Framework.

### Licensing

An important aspect of releasing software are the license restrictions which an API might implement. Both the OpenGL and Direct3D APIs have a licensing model which allows a developer to use the APIs in a commercial product without restrictions.

To release commercial software which implements the XNA Framework 2.0, a license agreement must be agreed upon between the developer and Microsoft which prohibits the usage of the network code provided by the XNA framework. The XNA Game Studio may not be used to create commercial titles for Xbox 360 but commercial Windows titles may be released. To distribute titles on the Xbox 360 platform, a $99.00 fee must be paid in order to be able to access the functionality provided by the XNA Creator's Club.

| Features | OpenGL | Direct3D | XNA |
|----------|--------|----------|-----|
Cross-Platform Support, amount | Yes, numerous | Yes, three | Yes, two
Learning Curve | High | High | Low
Native Language | C | C | C#
Supported Languages | Most Languages | Most Languages | .NET Languages
High Performance | Yes | Yes | No
License Restrictions | No | No | Yes
Support by Developer | No | Yes, paid | Yes, paid
Library Platform | Native | Native | Managed
