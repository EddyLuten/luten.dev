---
title: C Bitwise Operations Cheat Sheet
date:  2011-01-21 00:00:00 -0700
layout: single
---

## Operations Table

| Operation | Sample | C Operator |
---|---|---
AND | 1001 AND 0101 = 0001 | `&` (ampersand)
OR | 1001 OR 0101 = 1101 | `|` (pipe)
NOT | NOT 1001 = 0110 | `~` (tilde)
XOR | 1001 XOR 1011 = 0010 | `^` (caret)
LEFT-SHIFT | LEFT-SHIFT 0001 BY 1 = 0010 | `<<`
RIGHT-SHIFT | RIGHT-SHIFT 1000 BY 1 = 0100 | `>>`

## C Assignment Operators

| Operation | Syntax | Short For |
---|---|---
AND | `X &= Y;` | `X = X & Y;`
OR | `X |= Y;` | `X = X | Y;`
XOR | `X ^= Y;` | `X = X ^ Y;`
LEFT-SHIFT | `X <<= Y;` | `X = X << Y;`
RIGHT-SHIFT | `X >>= Y;` | `X = X >> Y;`

## Setting and Checking Bit-Flags

```c
#include <stdlib.h>
#define FLAG_ONE 0x0001     /* 0001 */
#define FLAG_TWO 0x0002     /* 0010 */
#define FLAG_THREE 0x0004   /* 0100 */

int main(void)
{
  unsigned int Flags = 0x0000; /* Initialize to zero */
  Flags |= FLAG_ONE;           /* Flags now contains 0001 */
  Flags |= FLAG_THREE;         /* Flags now contains 0101 */

  /* will return EXIT_SUCCESS since we never set FLAG_TWO: */
  return (Flags & FLAG_TWO) ? EXIT_FAILURE : EXIT_SUCCESS;
```
## Counting Set Bits

```c
#include <stdlib.h>
#include <stdio.h>
#define BITS_PER_INT ( sizeof(unsigned int) * 8 )
 
int main(void)
{
  unsigned int Flags = 0x0115; /* Dec: 277, Bin: 100010101 */
  unsigned int Mask = 0x0001;
  unsigned int Count = 0;
  unsigned int i = 0;

  for (i = 0; i < BITS_PER_INT; ++i, Mask <<= 1)
    if (Flags & Mask)
      ++Count;

  // The following line should print: Flags contains 4 set bits.
  printf("Flags contains %d set bits.\n", Count);
  return EXIT_SUCCESS;
}
```
