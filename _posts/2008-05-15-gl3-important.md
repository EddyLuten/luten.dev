---
title: Why OpenGL 3.0 is Important
date:  2008-05-15 00:00:00 -0700
layout: single
tags: [OpenGL]
---

Some questions have come up in regards to my last post, The Ghost of OpenGL 3.0, and one of them keeps popping out on top: Why do we need OpenGL 3.0 and What's wrong with OpenGL 2.1? This post will attempt to take you through the pre-published materials on the OpenGL API, version 3.0 and show you the major changes and differences. Or you could simple jump to the answer and conclusion without reading the features provided by OpenGL 3.0, if you don't feel like getting informed.

Terms used:

* Mutable: something which can change shape or form.
* Immutable: something which cannot change shape or form.
* API: Application Programming Interface, an interface designed to allow transactions with a library or application.

## Hardware Evolution

Besides being a graphics API, OpenGL sets a standard for IHVs (Independent Hardware Vendors) to comply with. By doing this, we can be sure that a certain type of hardware is compliant with a specific set of demands, not unlike what Microsoft has been doing with DirectX 10 and higher, albeit not an open standard. For example, OpenGL 2.0 formally introduced the GLSL (OpenGL Shading Language) which was not available in 1.5, thus forcing IHVs to implement the capabilities according to the OpenGL standard.

A comparison with the Direct3D side of things would be the enforcement of Direct3D 10.1 compliance by setting a mandatory requirement of 4x anti-aliasing.

OpenGL 3.0 is said to be able to function on OpenGL 2.1/DirectX 9 level hardware, so basically anything from the GeForce FX series and upwards (supporting High Level shaders).

## The Software Side

The OpenGL logoMost of the readers here are programmers, so the hardware side of the OpenGL standard will probably be less interesting to you than the features OpenGL 3.0 will bring. We all know that the OpenGL 3.0 specification has not yet been finalized, so all material discussed here is subject to change and compiled from various sources which I will list at the end of the post.

## Objects

One of the major changes that OpenGL 3.0 will introduce is the usage of objects. Yes, the specification is still specified through the C programming language which natively does not support the OOP (Object Oriented Programming) paradigm but a way around this is being implemented.

The objects themselves are similar to native C structs which are used for creating user-defined data-types. Please note that I refrain from using the word class since a class is a data-type on its own, not found in the C programming language nor used in combination with the OpenGL API.

So far, four object categories have been announced, namely:

* Templates
  * Put in simple terms: a placeholder for the definition of a specific object type. Attributes can be set to fulfill the creation of a specific object type. For example, to create an "image" object, one must first create a template object with specific parameters for the creation of the image object, set the attributes required for the object and pass it to an image object constructor function, e.g.: glCreateTemplate(GL_IMAGE_OBJECT); returns a GLtemplate object, after which attributes are applied, glCreateImage(variable to GLtemplate object); returns the handle to an image object (see Data Objects below) constructed according to the attributes supplied to the image template. Templates may be modified at any time since they are defined and stored on the client-side.
* State Objects
  * State Objects are simple objects containing a specific set of attributes applicable to multiple objects. State Objects are partially mutable once created, meaning that only certain aspects of the object can be altered after it has been constructed.
    Data Objects
  * The example given above at Templates talked about an "image object" which contains image data, stored in a Data Object. These objects have an immutable structure but the data is mutable. These Data Objects get stored VRAM (or RAM depending on the implementation) and can be shared amongst multiple contexts. Examples of Data Objects are Image Objects and Buffer Objects.
* Container Objects
  * The best way to describe a Container Object is by the example of the VAO (Vertex Array Object). The VAO represents a piece of geometry by describing an array of vertices stored in memory and may not be referenced amongst multiple contexts. The Container Object contains a mutable attachment (VAO: Vertex Buffer) and immutable attachment properties.

This new object-based system seems to be the biggest part of the restructuring of the standard and it certainly opens up a new realm of possibilities for IHVs/driver implementers. By abstracting the objects to the server-side, the underlying driver code can be optimized to handle the new data-types more efficiently. The more the API pushes to the server-side, the better the performance can potentially be optimized.

## Asynchronous Transactions

While this basically falls under the "Objects" heading, it's a feature worth mentioning alone. In an effort to improve parallelism, Object creation calls are asynchronous. This means that during the time that an object is being created, a valid handle to the object has already been returned for usage, even before the object's resources have actually been allocated.

What this means is that more commands can be executed on the client side while the server-side takes care of the execution thus resulting in a faster command chain.

## Backwards Compatibility

The OpenGL API has always been backwards compatible throughout its revisions and OpenGL 3.0 will not be an exception. Plans have been made to retain backwards compatibility with the current OpenGL 2.1 standard without breaking older applications.

Another feature, which has not been set in stone, is the manner of interoperability between OpenGL 3.0 and 2.1 which would allow an OpenGL 2.1 application to attain an OpenGL 3.0 rendering context.

## Goodbye, Fixed Function Pipeline

OpenGL 3.0 removes the fixed function pipeline which was eradicated in the Direct3D API in version 10. This means that many parts of a normal graphics pipeline are now programmable. This is a huge shift towards the future of a fully-programmable graphics pipeline which would be the definitive step in perfecting a graphics API.

The removal of the so-called "fixed function" pipeline means that all graphical output has to be defined through the "programmable pipeline" though a mechanism often called "Shaders." Shaders are programmed in a language called the OpenGL Shading Language (GLSL or glslang) or through an intermediary language such as Cg. Shaders not only allow for shading the geometry but also the transformation of its vertices (vertex shader) and individual pixels (fragment shader).

If you've read the heading above this one, you'll notice that OpenGL 3.0 is backwards compatible with older versions which support the fixed pipeline functionality. OpenGL also supports these functions but internally these are transformed into the form of shaders.

OpenGL version "Mount Evans", which will be released after OpenGL 3.0, will support the functionality provided by Geometry Shaders which allows for the manipulation of "pieces" of geometry and generation of new geometry as well. This allows the programmer to take advantage of currently available hardware-accelerated functionality such as tessellation. Even though this functionality is said to be provided after 3.0 has been released, it is likely that this functionality will be provided with the formal release of OpenGL 3.0 instead.

## So, what's wrong with 2.1?

By now you might have noticed that I haven't exactly formally answered the question "What's wrong with OpenGL 2.1?" The answer is: There's nothing wrong with OpenGL 2.1.. informally. OpenGL 2.1 is a very capable API which could support many of the features that OpenGL 3.0 incorporated. The big difference is of course that the functionality in OpenGL 3.0 will be a formal standard while the 3.0-like functionality in OpenGL 2.1 is provided through IHV-developed OpenGL extensions which may differ from one and other.

The above, and the fact that the new API works with Objects, is causing the anticipation. OpenGL 3.0 will formally push the API into the next-generation era and will finally be able to compete with Direct3D 10, which is why OpenGL 3.0 is important.

## Conclusion

As said above, OpenGL 3.0 will push the API into the next generation. In my personal opinion, the new structure of OpenGL 3.0 could severely compromise the position of Direct3D in the Microsoft Windows gaming market since the functionality provided with OpenGL 3.0 will also work on Windows XP, unlike Direct3D 10. Vista is still being viewed upon as somewhat of a quirky Operating System and many developers and users are sticking with XP for the time being.

I'd like to conclude by saying that this post does not present all of the new published features in OpenGL 3.0, rather it lists the features which I find most compelling about the new API. Also, I'm not affiliated with the Khronos Group in any way so everything you read here is non-official and compiled from various online sources, talking about the unfinished and proposed API. Last but not least, I don't guarantee the correctness of the article, nor the correctness of the sources used — correct me if I'm wrong about something.

## Some old Comments

Taken from the original, now lost blog post comment section:

> Korval says;
> 16 May 2008 - 13:01
>
> Nobody really says that GL 3.0 isn't important. But the fact is that it's too late. There was a pretty good window of opportunity for a new and improved GL API to swoop in and garner attention among PC game developers. That time has passed. Vista adoption is up, which means that D3D10 usage will be up. The break between Vista/XP and D3D10/9 (ie: if you use XP, you can't have D3D10 features) was a good opportunity that the ARB has squandered.
>
> Furthermore, if the GL ARB couldn't get this done last year, why should we believe them this year? The fact is that the ARB has failed, monstrously. They did it before back when they were working on render-to-texture. They spent 2 years on something that shouldn't have taken more than 6. The younger GL programmers may not remember the days before VBO, but it took an awfully long time to get VBOs as well; until then, we had to rely on a bunch of vendor-specific extensions.
>
> I love the ideas behind GL 3.0; I even wrote my GL 2.1-based rendering abstraction layer based on those ideas. But the fact is that it's very, very late. And even that wouldn't be so much of a problem if they could just tell us WHY it's late. But they won't. Which means it's either IP or some stupid argument about something that matters very little. And if it's the latter, then that means that the ARB is so worried about making a mistake that they won't actually produce anything. Which makes them ineffective.
>
> For 1 year, the ARB was good about updating us on their progress. And then they stopped. That shows a blatant lack of respect for us the potential users of OpenGL. So why should we respect them back?

--

> Dave says;
> 19 May 2008 - 4:38
>
> I think exactly the same to #Korval.
>
> Every version of DirectX has the great disvantage of relying on a binary format for method calling and structs memory layout that is completely incompatible between major versions.
>
> OpenGL has a smarter design in the sense of using raw C functions (instead of virtual C++ like methods) and almost no C structs.
>
> But it is released with a functional equivalence to DX almost 2 years before. Otherways, using non-standar extensions is a nightmare.
>
> Current OpenGL version has a lot of inconsistences, and a lot of legacy unusefull methods.
>
> But the modern design of DX is not the only advantage over OGL, but a consistent DirectX SDK with a compact documentation and a pletoria of examples.

--

> Aras Pranckevičius says;
> 19 May 2008 - 13:06
>
> I don't mind D3D changing the API with each major revision. API itself is nothing; it's really easy to rewrite "the same stuff" to another API. Underlying hardware is still the same, so if the API is not Completely Stupid, it's not a big deal.
>
> What I do mind though, is whether API and everything related to it (drivers) work. OpenGL fails miserably in this regard, with it's approach of "let's let each IHV make their own bugs in the whole stack!" it's just horrible. FBOs? GLSL? Argh!
>
> Another thing that I don't mind that much is all the legacy APIs/extensions. There's probably ten ways to submit vertex data, while in fact there should be vertex buffers only. And even then, VBOs in GL don't match up what was available in D3D for years (updating a portion of VBO without additional memory copy, anyone?).
>
> So in my view GL3 does not bring anything new to the table. Ok, maybe it will be simpler for IHVs to implement, which would take care of some bugs in the drivers. But what they should really do is force a common stack upon everyone, and make only the lowest-level driver be a responsibility of IHV.
