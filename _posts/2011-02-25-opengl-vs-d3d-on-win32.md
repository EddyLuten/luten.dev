---
title: "OpenGL vs Direct3D: Where are we on Windows? (Win32)"
date:  2011-02-25 00:00:00 -0700
layout: single
---

It's almost weekend, and time for a lighthearted post on the two realtime 3D computer graphics libraries that are available on Windows in 2011: OpenGL and Direct3D. The reason I mention the year is simply because of the fact that two years from now, this information will be as untrue as the Wikipedia article[*](https://web.archive.org/web/20150223211220/http://en.wikipedia.org/wiki/Talk:Comparison_of_OpenGL_and_Direct3D) on this matter due to rapid hardware and software developments. But for now, let's bash it out.

## A (skippable) Condensed History

About ten years ago, in the first days of Windows XP (D3D 8.1 / GL 1.3), there wasn't a clear winner when it came to picking a realtime 3D library on Windows. Both OpenGL and Direct3D were viable libraries to use and it really wasn't until 2002 that OpenGL needed to pick up some slack when Direct3D 9.0 was released with support for high level shaders through HLSL (High Level Shader Language). In 2004, OpenGL 2.0 was released with GLSL (OpenGL Shading Language), and for a while the libraries were competing again on the PC.

That was until Windows Vista came around and introduced Direct3D 10, a complete rewrite of the Direct3D API that no longer allowed for fixed function pipeline calls, and relied solely on the usage of the programmable pipeline through buffer objects and shaders. The new library was slick, fast, and converted a great deal of Win32 OpenGL programmers into Direct3D programmers.

OpenGL fell behind and needed to catch up badly, but it was quiet on the OpenGL front until 2006/2007 when OpenGL 3.0 was announced as (also) a complete rewrite of the OpenGL API. After a long wait, OpenGL 3.0 was released against high community expectations in 2008.

However, OpenGL 3.0 wasn't at all what the community was promised and not a competitor to Direct3D 10. Community speculation/gossip suggested that the big CAD companies blocked the promised API overhaul, which turned out to be false. More Win32 OpenGL programmers were pissed and dropped the API in outrage, and switched to Direct3D instead.

In the meantime, Direct3D kept on evolving and became the de facto realtime 3D graphics API on the Windows platform while OpenGL stagnated on the PC but thrived on embedded systems (mobile phones, tablets, PS3, etc.) as OpenGL ES.

So now it's 2011 and we have Direct3D 11 and OpenGL 4.1 available to us. Both APIs increased one version since 2008, but how exactly do they compare? Let's take a look.

## General API Differences

A modern realtime 3D computer graphics library's main task is to expose the underlying hardware. Both OpenGL and Direct3D share similar features that I won't explore. Both libraries generate (pixel/fragment-, index-, vertex-) buffers with no real differences beside the look and feel of the API calls. Most calls result in the same output since the hardware and drivers don't change, i.e., the API it's simply a software layer on top of the driver.

## Comparison Table

Here's the quick and dirty rundown of some of the modern features that really differentiate the two APIs in 2011:

| Feature Support | OpenGL | Direct3D |
|---|---|---|
Thread Safe API | No, an OpenGL rendering context can only be safely referenced in the thread that created it. | Yes, since Direct3D 11.
Fixed Function API | Yes and No. OpenGL 3.1 deprecated the fixed function pipeline, but can still access it by creating a context using the "compatibility-profile”. | Removed from Direct3D 10.
Geometry Shaders | Yes, since OpenGL 3.2. | Yes, since Direct3D 10.
Tessellation | Yes, since OpenGL 4.0. | Yes, since Direct3D 11.
GPGPU | Not directly, but accessible through sister API OpenCL. | Yes, through Compute Shaders, a.k.a. DirectCompute.
Order-Independent Transparency | Not natively, but can be achieved through GPGPU.
Compiled Shader Saving/Loading | Yes, since OpenGL 4.1. | Yes, since Direct3D 9.
Cross-Platform Compatibility | Numerous, including sister API OpenGL ES 2.0 since OpenGL 4.1. | Yes, Xbox in Direct3D 8.1, Xbox 360 in 9.0c, and various Linux platforms through Wine (which wraps D3D calls around OpenGL).
Native Fonts/Text Rendering | Yes and No: "Yes” using WGL before OpenGL 3.1, or using the Compatibility Profile in later OpenGL versions. "No” if the Core Profile is selected due to deprecation of display lists. | Yes, in Direct3D 9 and 10 through D3DX, and through DirectWrite or Direct2D since Direct3D 11.
Enumeration of Device Capabilities and Modes | Yes, through various functions. | Yes since Direct3D 9 through Direct3D functions, but through DXGI since Direct3D 10.
Hardware Instancing | Yes, since OpenGL 3.0. | Yes since Direct3D 9, improved in Direct3D 10 with "Instancing 2.0".
Documentation | Yes, the specification is online in PDF form, but no real central repository of information. | Yes, the SDK documentation is available online as well as downloadable with many samples.

Both APIs have their strengths, but on Windows it's hard to ignore Direct3D 11 because of its tight connection to the operating system. While the latest version of OpenGL exposes next-gen features in Windows XP, this is not really a great feat in 2011. Many end users have moved on to Windows 7 and Vista where these features are available intrinsically.

OpenGL relies much on 3rd party libraries to handle non-rendering tasks such as creating font outlines and loading images. On the one hand, this is what makes OpenGL extremely portable, while on the other hand you are creating an additional dependency. I listed font support especially, since it such a shame that there is no replacement for `wglUseFontBitmaps` on core profiles, an incredibly easy-to-use extension on Windows. Yes, there is Freetype, but you're creating an external dependency.

When speaking of documentation, Direct3D is the clear winner with MSDN and the downloadable SDK containing samples, tutorials, help files, and binaries. OpenGL.org is just not a the friendliest site for developers, and while there have been recent improvements, the OpenGL SDK is not something to write home about. Besides that, it is great having the OpenGL and GLSL specifications available in PDF form, something that's not accessible to developers from Microsoft. Also, the extension repository is a great help, albeit difficult to browse.

## Conclusion

Personally, I feel that OpenGL is far behind Direct3D on Windows, and it's a shame. I prefer OpenGL's pure C API and naming conventions over that of Direct3D's, but I see really no incentive to use it anymore. And if it wasn't for GLEW or GLee, OpenGL would be a pain to use with Windows' OpenGL 1.1 header file (not OpenGL's fault).

So in conclusion, it comes down to the old advice that doesn't seem to change much over the years:

* If you are creating software that runs solely on Windows and potentially Xbox, you need Direct3D.
* If you create software that needs to run on a wide variety of platforms, you need OpenGL.
* If you support Windows and other platforms as well, use Direct3D on Windows and OpenGL on the other platforms.
