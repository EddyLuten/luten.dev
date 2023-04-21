---
title: Amount of Digits in an Integer
date:  2008-10-12 00:00:00 -0700
layout: single
tags: [C, Tutorial]
---

Here's another little snippet that might come in handy in your programmatic travels. I'll show you an example of usage below, which might also be of interest to you. The code presented is in C, not C++. First, the code to count the amount of digits in an integer:

<!--more-->

```c++
const size_t intlen(long long int Num)
{
  size_t out = 1;
  while (Num /= 10) ++out;
  return out;
}; // numlen
```

Looks simple enough; simply count the amount of times we can divide the number by 10 without the result being zero. This function takes a copy of an int (or long long) so that we don't have to copy the number inside the body of the function and returns a size_t (unsigned int).

As for the usage example, it's a bit more complex and might seem a bit "obfuscated" at first, but fear not, I will explain below.

```c++
void inttoa(long long int Num, char** RetVal)
{
  size_t neg = (Num < 0);
  size_t len = intlen(Num) + (neg ? 1 : 0); // add one for the "-" character
  size_t i;

  *RetVal = (char *) malloc(sizeof(char) * (len + 1));

  if (NULL == (*RetVal))
    return; // bad malloc

  if (neg)
    Num = -Num; // make pos if neg

  for (i = len; i; (Num /= 10), --i) // loop backwards
    (*RetVal)[i-1] = (char)((Num % 10) + '0'); // add modulo to char zero

  if (neg)
    (*RetVal)[0] = '-'; // first char

  (*RetVal)[len] = 0; // last char, null terminator
}; // intttoa
```

As you might have suspected, this function converts an integer to character string. First, we determine if the number is negative and retrieve its length with the help of the previous function. We allocate a character string with the length determined and start appending a character to the string.

You can use it like so:

```c++
char* mystring; // don't allocate, don't do anything
inttoa(42, &mystring); // simply pass it to the function

// do things with the string

free(mystring); // you *do* have to free() the string though
```
