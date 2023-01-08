---
title: "BC42104: Variable ‘X' is used before it has been assigned a value."
date:  2011-02-11 00:00:00 -0700
layout: single
---

My dearest VB.NET programmers (and C# programmers up to a point), I once again have to inform you of one of my pet peeves. This is pretty much a follow-up to one of my previous posts, but more than two years after, I still work in projects from various online sources as well as professionally that are littered with the warnings about undefined variables:

<!--more-->

```text
warning BC42104: Variable 'X' is used before it has been assigned a value. A null reference exception could result at runtime.
```

At runtime, these warnings usually translate into the dreaded `NullReferenceException`:

```text
NullReferenceException was unhandled, Object Reference not set to an instance of an object.
```

So, what causes this and how can can we fix this? Let's take a look at a piece of code that demonstrates something incredibly common, especially in VB circles:

```vb
Dim MyString As String

If ThisAndThat Then
    MyString = "Some Value"
End If

...

SomeFunction(MyString)
```

If the boolean `ThisAndThat` evaluates to `False`, `MyString` will never be defined, and a `NullReferenceException` will arise when the `SomeFunction` function tries to do anything with `MyString`. Remember that The `System.String` class does not have a default constructor, so no constructor is implicitly called. `MyString` is NOT `String.Empty`, but `NULL`.

To fix this, all you need is an `Else` statement in your code and some default value that you'd like to assign to `MyString`:

```vb
Dim MyString As String

If ThisAndThat Then
    MyString = "Some Value"
Else
    MyString = String.Empty
End If

...

SomeFunction(MyString)
```

In fact, the best way to handle default values is to define the variable upon declaration:

```vb
Dim MyString As String = String.Empty

If ThisAndThat Then
    MyString = "Some Value"
End If

...

SomeFunction(MyString)
```

Or you could even eliminate the If statement entirely by using the `IIf` function:

```vb
Dim MyString As String = IIf(ThisAndThat, "Some Value", String.Empty).ToString()

...

SomeFunction(MyString)
```

And even though I'm using the class `System.String` as an example, this should be applicable to any variable of any data type. It's a good practice and will eliminate many of those pesky runtime errors that can be difficult to trace.
