---
title: C++ PImpl Template
date:  2013-02-23 00:00:00 -0700
layout: single
---

If you're not familiar with the PImpl (private implementation) idiom, read [this Wikipedia article](https://web.archive.org/web/20150222044000/http://en.wikipedia.org/wiki/Opaque_pointer) first. While this is more or less "syntactic sugar" since the templates are expanded during compilation, but I think it makes for cleaner looking code.

<!--more-->

## Classic PImpl

Usually, while forward declaring the pimpl struct or class, we do something like this:

```c++
class MyClass
{
  struct Implementation;
  MyClass::Implementation* pimpl;

public:
  MyClass();
  ~MyClass();

  void DoAllTheThings();
};
```

And the following definition:

```c++
#include "MyClass.h"

struct MyClass::Implementation
{
  int foo;
  int bar;
}
```

## PImpl\<T\>

There's absolutely nothing wrong with that, but consider the following reusable template:

```c++
template<typename T>
struct PImpl
{
protected:
  struct Implementation;
  Implementation* pimpl;
};
```

And the following implementation of the template:

```c++
#include "PImpl.h"

class MyClass :
  public PImpl<MyClass>
{
public:
  MyClass();
  ~MyClass();

  void DoAllTheThings();
};
```

And the following source file definition:

```c++
#include "MyClass.h"

template<>
struct PImpl<MyClass>::Implementation
{
  int foo;
  int bar;
};
```

There is no forward declaration of the struct in `MyClass`, only public inheritance of `Pimpl<T>` and the implementation in the source file is nearly identical.
