---
title: Flattening Multidimensional Arrays
date:  2008-10-11 00:00:00 -0700
layout: single
tags: [C, Tutorial]
---

**Edit:** Thank you, fixitman for the insightful comment; the code has been fixed to work with non-square arrays as well.

In an effort to produce a better performing multidimensional array, I would like to share the following with you. Say we have a Matrix (or multidimensional array) of 5 x 5 integer elements, M. In order to allocate such an array in C++, we use the following code:

<!--more-->

```c++
const size_t Width = 5;
const size_t Height = 5;
int** Array = new int*[Height]; // 2-Dimensional

for (size_t i = 0; i < Height; ++i)
  Array[i] = new int[Width];

// etcetera.

for (size_t i = 0; i < Height; ++i)
  delete[] Array[i];
delete[] Array;
```

In order to counter-act this looping behavior, which, in many cases will slow down the program upon allocation and freeing of memory (due to the loops), the array may be flattened like so:

```c++
const size_t Width = 5;
const size_t Height = 5;
int* Array = new int[Width*Height]; // 1-Dimensional

// etcetera.

delete [] Array;
```

Thus causing fewer allocations than before, and eliminating loops entirely. You might think that the array is entirely out of order, and no logical index can be obtained for selecting e.g.: `Array[2][3];`. This is where a simple calculation comes in handy.

A<sub>X</sub>,<sub>Y</sub> = (Y x Width) + X

With this calculation we can select our element by doing the following:

```c++
//...
// desired position:
const size_t X = 2;
const size_t Y = 3;
//...
int RequestedInteger = Array[(Y*Width)+X];
```

O| 0| 1| 2| 3| 4|
0| 0| 1| 2| 3| 4
1| 5| 6| 7| 8| 9
2| 10| 11| 12| 13| 14
3| 15| 16| 17| 18| 19
4| 20| 21| 22| 23| 24

This works because if we visualize our flattened array’s indexes in a table (above), we can see that if we take Y (3) and multiply it by the Width (5) we get the appropriate first index of the row (15, or 0,3). If we add X (2) we have selected index 17, which is the index we want (X<sub>2</sub>, Y<sub>3</sub>).

This implementation is faster because we only allocate one single block of memory of X\*Y instead of X\*Y blocks of memory. The disadvantage of this is that to select any index from the array, you will have to calculate the expression, but this is a minor operation compared to the allocation/de-allocation loops.
