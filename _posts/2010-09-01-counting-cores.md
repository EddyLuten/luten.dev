---
title: Counting Processor Cores and Threads
date:  2010-09-01 00:00:00 -0700
layout: single
tags: [C, Tutorial, Win32]
---

Here's a little snippet I'd like to share with you since there really isn't a good example online that shows you how to count the processor cores and threads on Microsoft Windows using the Windows API through C++.

<!--more-->

If you have the need to count cores, or if you wish to determine if the system running your program is multicore, this snippet can come in handy.

By “counting threads” I mean counting the logical processors present, since Hyper-Threaded processors may display multiple logical cores per physical core — counting these is the tricky part.

Here's the entire program for your copy and paste convenience, we'll discuss it step-by-step below the snippet if you're interested:

```c++
#include <iostream>
#include <windows.h>

int main(void)
{
  unsigned Cores = 0;
  unsigned Threads = 0;
  PSYSTEM_LOGICAL_PROCESSOR_INFORMATION buffer = NULL;
  DWORD Size = 0;

  GetLogicalProcessorInformation(buffer, &Size);
  if (ERROR_INSUFFICIENT_BUFFER != GetLastError())
    return -1;

  buffer = new SYSTEM_LOGICAL_PROCESSOR_INFORMATION[Size];
  if (FALSE == GetLogicalProcessorInformation(buffer, &Size))
  {
    delete [] buffer;
    return -1;
  }

  const size_t Elements =
    Size / sizeof(SYSTEM_LOGICAL_PROCESSOR_INFORMATION);

  for (size_t i = 0; i < Elements; ++i)
  {
    if (buffer[i].Relationship == RelationProcessorCore)
    {
      ++Cores;

      if (buffer[i].ProcessorCore.Flags == 1)
      {
        int mask = 0x1;
        const size_t IntBits = 8 * sizeof(ULONG_PTR);

        for (size_t j = 0; j < IntBits; ++j, mask <<= 1)
          if (buffer[i].ProcessorMask & mask)
            ++Threads;
      }
    }
  }

  delete [] buffer;

  std::cout
    << "This system contains " << Cores << " core(s) and "
    << Threads << " thread(s)" << std::endl;

  return 0;
}
```

Well, that's quite a bit of code without any comments, so here's the explanation.

The first thing we do is define a few variables, which will contain the amount of Cores, Threads, a processor information array (the variable named “buffer”), and the size of the array:

```c++
unsigned Cores = 0;
unsigned Threads = 0;
PSYSTEM_LOGICAL_PROCESSOR_INFORMATION buffer = NULL;
DWORD Size = 0;
```

No difficulty there, now let's poll `GetLogicalProcessorInformation`, and ignore its return value just to get the size of the array that we should allocate:

```c++
GetLogicalProcessorInformation(buffer, &Size);
if (ERROR_INSUFFICIENT_BUFFER != GetLastError())
  return -1;
```

Notice that we don't entirely ignore errors which the function may throw, since we poll windows for the last error, and expect `ERROR_INSUFFICIENT_BUFFER`, which we expect in the first place. Now that we have obtained the size of the array, it's time to allocate it and fill it out with processor information:

```c++
buffer = new SYSTEM_LOGICAL_PROCESSOR_INFORMATION[Size];
if (FALSE == GetLogicalProcessorInformation(buffer, &Size))
{
  delete [] buffer;
  return;
}
```

In this case, we do check for erroneous return values and exit the application if we encounter any. Next we count the number of actual `SYSTEM_LOGICAL_PROCESSOR_INFORMATION` instances present in the array and loop through them one by one.

```c++
const size_t Elements =
  Size / sizeof(SYSTEM_LOGICAL_PROCESSOR_INFORMATION);

for (size_t i = 0; i < Elements; ++i)
{
```

We're looping through the array and checking if the encountered `SYSTEM_LOGICAL_PROCESSOR_INFORMATION` instance contains processor core information by checking if the `relationship` flag equals `RelationProcessorCore`. If it does, we increment the Cores variable and check if ProcessorCore.Flags is set to one, since this signifies the presence of logical cores in the case of Hyper-Threading:

```c++
if (buffer[i].Relationship == RelationProcessorCore)
{
  ++Cores;

  if (buffer[i].ProcessorCore.Flags == 1)
  {
```

This is where the magic happens and we count the amount of logical processing units by checking if some bits are set to 1 in an integer.

```c++
int mask = 0x1;
const size_t IntBits = 8 * sizeof(ULONG_PTR);

for (size_t j = 0; j < IntBits; ++j, mask <<= 1)
  if (buffer[i].ProcessorMask & mask)
    ++Threads;
```

If you didn't follow the above snippet because of the bit manipulation, let me break it down for you. The first line defines the mask that we're going to be testing with, and looks like this in binary:

```text
0000 0000 0000 0000 0000 0000 0001
```

The next variable (`IntBits`) contains the calculated amount of bits in a `ULONG_PTR`. This number is usually 32, but let's calculate it anyway to be absolutely certain. Since `sizeof()` returns the size of something in bytes, we multiply by eight to get the amount of bits, since there are eight bits in a byte.

Next, we start a new loop using iterator `j` to loop through the bits in `ProcessorMask`. Upon each iteration of the loop, we increment the iterator and shift the bits in the mask one position to the left so that the mask after the first iteration would look like this in binary:

```text
0000 0000 0000 0000 0000 0000 0010
```

Inside of our loop, we test if the position indicated by our mask is present in the `ProcessorMask`. This is best illustrated by using the binary notation above. For example, let's say we have two threads for the current core. The variables would be tested like so:

```text
First Iteration (j = 0):
0000 0000 0000 0000 0000 0000 0011 (ProcessorMask)
0000 0000 0000 0000 0000 0000 0001 (mask)
------------------------------------ AND
0000 0000 0000 0000 0000 0000 0001 = 1
```

Since the value returned is either zero or not zero, it can be converted into a boolean value. This means that we can increment the `Threads` variable if the value is not zero, but don't if the value is zero.

Here's an example of when all of the bits in the `ProcessorMask` have been tested and the next value is zero, thus evaluates to a boolean false (notice the bit-shifted mask variable):

```text
Third Iteration (j = 2):
0000 0000 0000 0000 0000 0000 0011 (ProcessorMask)
0000 0000 0000 0000 0000 0000 0100 (mask)
------------------------------------ AND
0000 0000 0000 0000 0000 0000 0000 = 0
```

The above section is the meat and potatoes of the application, and is how you count cores and threads. The code that follows closes the loops and deletes the buffer since we no longer require it to be allocated.

This concludes the snippet, I hope it was helpful to you (post questions if you have any!). If you wish to learn more about the functions used, here are links to the appropriate manual entries on MSDN:

* [GetLogicalProcessorInformation](https://web.archive.org/web/20101005084903/http://msdn.microsoft.com/en-us/library/ms683194.aspx)
* [SYSTEM_LOGICAL_PROCESSOR_INFORMATION](https://web.archive.org/web/20101005084903/http://msdn.microsoft.com/en-us/library/ms686694.aspx)
* [GetLastError](https://web.archive.org/web/20101005084903/http://msdn.microsoft.com/en-us/library/ms679360.aspx)
