---
title: "Creating a Window Wrapper Class: Redux"
date:  2010-09-13 00:00:00 -0700
layout: single
---

Okay, so I know you're probably here because you searched for "window wrapper class" or something similar and expected the article that I use to host on Scriptionary that threw a bunch of C++ code at you for you to copy and paste. I regret to inform you that the article you were looking for has ceased to exist.

Sorry about that.

However, in its place I have for you this very post which will teach you how to accomplish creating such a wrapper all by yourself. I hope that is okay since all you really need to know is the how to create a window procedure that you can use with your custom class.

<!--more-->

## The Window Procedure

The window procedure is a function that is tied to a window upon creation. This function handles the window's events (also: messages, notifications) such as `WM_PAINT`, `WM_SIZE` and a plethora of others that a window can throw at you. The trick is to pass a function callback to `WNDCLASS` or `WNDCLASSEX` that is part of your class, which is pretty much impossible since you can't pass instance members by reference. Let's take a look at a standard windows procedure:

```c++
LRESULT CALLBACK WndProc(
  HWND hwnd,
  UINT message,
  WPARAM wParam,
  LPARAM lParam)
{
  switch (message)
  {
  case WM_PAINT:
    // handle event
    return 0;
  /* many more possible events */
  default:
    return DefWindowProc(hwnd, message, wParam, lParam);
  }
}
```

Well, that's pretty much as plain as Windows functionality gets, so nothing too special there. Let's make this function a member of our imaginary class Window since no matter what, we will need a regular WndProc that will handle our events:

```c++
class Window {
  // *snip*
  LRESULT CALLBACK LocalWndProc(
    HWND hwnd,
    UINT message,
    WPARAM wParam,
    LPARAM lParam
  );
};
```

Since we can't pass member functions to serve as callbacks, we'll have to do it the C+ way (somewhere between C and C++). For this we'll need the feared static keyword, which signifies that the function is shared by all of the instances of our imaginary Window class:

```c++
class Window {
  // *snip*
  static LRESULT CALLBACK StaticWndProc(
    HWND hwnd,
    UINT message,
    WPARAM wParam,
    LPARAM lParam
  );
};
```

You may not realize it, but we've already defined the hardest part of the entire window wrapper. Since `StaticWndProc` is static in nature, we can pass it as a function callback since it's not bound to a specific instance of our Window class — almost like a global function.
User Data

You may wonder: Okay, so how do I make this static function specific to my current instance? And most importantly, how do I get from the `StaticWndProc` back to the regular `LocalWdnProc`?

Well, this is where we're lucky that the Windows API provides us with a bit of leeway. Let's take a look at the `CreateWindow` function prototype straight from the MSDN documentation:

```c++
HWND WINAPI CreateWindow(
  __in_opt  LPCTSTR lpClassName,
  __in_opt  LPCTSTR lpWindowName,
  __in      DWORD dwStyle,
  __in      int x,
  __in      int y,
  __in      int nWidth,
  __in      int nHeight,
  __in_opt  HWND hWndParent,
  __in_opt  HMENU hMenu,
  __in_opt  HINSTANCE hInstance,
  __in_opt  LPVOID lpParam
);
```

The last parameter, `lpParam`, allows us to pass custom data to the window procedure which is accessible when the `WM_NCCREATE` event is active. This means that when we pass `static_cast<void*>(this)` into `lpParam`, we can pick that data back up in our static window procedure.

The problem is that this data doesn't persist beyond the `WM_NCCREATE` event, so we need to find a way to store it somewhere permanent; this is where that leeway that I mentioned before comes in.

If you've never heard of the constant `GWLP_USERDATA` I don't blame you since there's not much documentation about at MSDN. `GWLP_USERDATA` is a constant passed to the `SetWindowLongPtr` and `GetWindowLongPtr` functions, providing access to a pointer-sized chunk of memory attached to your window.

So when we process `WM_NCCREATE`, we'll grab the `lpParam` pointer passed to `CreateWindow`, and set it as user defined window data by using `SetWindowLongPtr` with `GWLP_USERDATA`:

```c++
LRESULT Window::StaticWndProc(
  HWND hwnd,
  UINT message,
  WPARAM wParam,
  LPARAM lParam)
{
  // Check if we're currently creating the window:
  if (message == WM_NCCREATE)
    SetWindowLongPtr(
      hwnd,
      GWLP_USERDATA,
      reinterpret_cast<LONG_PTR>(
        reinterpret_cast<LPCREATESTRUCT>(lParam)->lpCreateParams
      )
    );

  // Retrieve the data stored in the WM_NCCREATE event and
  // cast it to a Window pointer:
  Window* UserWindow = reinterpret_cast<Window*>(
    GetWindowLongPtr(hwnd, GWLP_USERDATA)
  );

  // If the data returned was NULL, default to the by windows
  // provided default window procedure:
  if (NULL == UserWindow) {
    return DefWindowProc(hwnd, message, wParam, lParam);
  } else {
    return UserWindow->LocalCallback(hwnd, message, wParam, lParam);
  }
}
```

## Conclusion

Let's review the entire process step by step:

* Pass the static callback into the `WndProc` member of the `WNDCLASS` structure for your window,
* Pass a this pointer into the `lpParam` parameter of the `CreateWindow` function,
* Retrieve the pointer when handling the `WM_NCCREATE` event and store it with `SetWindowLongPtr` using the `GWLP_USERDATA` constant,
* After that, retrieve the pointer to your window using `GetWindowLongPtr` using the `GWLP_USERDATA`, cast it back to your window class and call the local window procedure.
