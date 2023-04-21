---
title: "C++ Events with lambda expressions, and std::function"
date:  2011-07-05 00:00:00 -0700
layout: single
tags: [C, Tutorial]
---

One of the things that C++ doesn't have out-of-the-box is events, which is not necessarily a bad thing. However, with the additions to the C++0x/C++11 specification, we can implement something like an event system found in higher level languages such as C# using relatively easy to use code.

<!--more-->

Please note that this is not the Observer pattern, and this may not be the best way of handling events — though it's easy to comprehend.

The main things that we're going to use from the new spec are:

* Lambda expressions
* std::function wrappers

All of the other code is plain old vanilla C++ 2003.

With function wrappers, we can define the signature of our event-handers, so if we wanted an even handler named OnSomethingHandler, we could define it like so:

```c++
typedef std::function<void(void)> OnSomethingHandler;
```

Where the `OnSomething` event takes no parameters, and returns nothing either. Let's define a class that dispatches these `OnSomething` events and name it Foo:

```c++
#include <functional>
#include <vector>

class Foo
{
public:
  typedef std::function<void(void)> OnSomethingHandler;

  Foo()
  {
  }

  void AddOnSomethingHandler(OnSomethingHandler Handler)
  {
    handlers_.push_back(Handler);
  }

  void TriggerOnSomethingEvents(void)
  {
    for(auto i = handlers_.begin(); i != handlers_.end(); ++i)
      (*i)();
  }

private:
  std::vector<OnSomethingHandler> handlers_;
};
```

That should be pretty easy to follow, you add new event handlers to the class that calls the events by calling `Foo::AddOnSomethingHandler`, the events are then triggered by the call to `Foo::TriggerOnSomethingEvents`.

If this seems a bit abstract to you, imagine the Foo class to be called `Window`, `Foo::OnSomethingHandler` called `OnResizeHandler`, and `Foo::TriggerOnSomethingHandler` called `Resize`, and you'll get the picture.

If you haven't been exposed to C++0x, std::function may seem a bit alien. Simply put, std::function is a function wrapper, whose wrapped function is called by invoking the parentheses () operator, which will take parameters as well if any were required (none in our case). You can use this template after including the functional header file, part of C++0x, but available in most STL distributions even now.

Now that we have our event-dispatching class, let's figure out how to add event handlers. First, let's explore trivial events, that maybe don't really require their own function at all. Maybe a one-liner that writes something to the console.

```c++
#include <iostream>
#include <functional>
#include <vector>

// ... Foo definition ...

int main()
{
  Foo my_foo;

  my_foo.AddOnSomethingHandler([](){
    std::cout << "Hello, World!" << std::endl;
  });

  // etc.

  my_foo.TriggerOnSomethingEvents();

  return 0;
}
```

When `my_foo.AddOnSomethingHandler` is called, there is a strange new syntax that you may not have seen before:

```c++
[](){ /* ... */ }
```

This is called a lambda expression, which is C++'s version of an anonymous function. These lambdas can be passed around a program using the std::function wrapper, or stored in a variable. This means, that we could have written the example above like this as well:

```c++
Foo::OnSomethingHandler my_handler = [](){
  std::cout << "Hello, World!" << std::endl;
};

my_foo.AddOnSomethingHandler(my_handler);
```

However, in real-world applications, there's often a need to use class member functions. Let's also define class `Bar`, which contains a member-function to handle the `OnSomething` event:

```c++
class Bar
{
public:
  Bar(Foo& foo)
  {
  }

  void MyOnSomethingEventHandler(void)
  {
    std::cout << "Hello, World From Bar!" << std::cout;
  }
};
```

While the member function `Bar::MyOnSomethingEventHandler` has the proper return type and parameter list to be considered a `Foo::OnSomethingHandler`, it is a member function, and we cannot pass member functions around as parameters unless we declare `Foo::OnSomethingHandler` to explicitly use `Bar::MyOnSomethingEventHandler` functions, which is something undesirable. To get around this limitation, we employ a lambda expression. Consider the new constructor for `Bar`:

```c++
Bar(Foo& foo)
{
  foo.AddOnSomethingHandler([this](){
    this->MyOnSomethingEventHandler();
  });
}
```

In this version, the lambda expression contains a "capture clause," explicitly capturing the this pointer. Anything captured in this clause can be used inside of the lambda expression's body, and anything that isn't captured can't be used. Inside of the lambda expression's body, you can now reference the pointer, and call the member function with ease. As long as the this pointer is valid (meaning that as long as your instance of `Bar` does not go out of scope) your lambda expression will function properly.

## Final Thoughts

There may be better ways of handling events, but as a way to introduce the concept of lambda expressions and the std::function template, performance is of no concern. If you care about small memory footprint and high performance code, you're still better off writing your own event system using function pointers wrapped in your own specialized wrappers. The STL isn't known for its high performance, after all.

Running in debug mode, in my implementation of the STL (Visual C++ 2010 SP1), the std::function wrapper used above uses 24 bytes of memory, which is quite excessive for a what can be implemented using function pointer. However, unless you write code that is ultra performance critical in debug mode, uses hundreds or thousands of events, and can't spare a few extra bytes on each callback, this shouldn't be an issue. Some performance testing on lambdas and the std::function template would be helpful, but I couldn't find anything substantial just yet.

* [More information about lambda expressions @ MSDN](https://web.archive.org/web/20150222043950/http://msdn.microsoft.com/en-us/library/dd293603.aspx)
* [More information on the functional header file](https://web.archive.org/web/20150222043950/http://www.cplusplus.com/reference/std/functional/)
