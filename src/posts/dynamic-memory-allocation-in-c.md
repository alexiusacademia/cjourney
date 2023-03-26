---
title: Dynamic Memory Allocation in C
description: Demystifying the dynamic memory allocation in C allowing developers
  to create features found on higher level languages such as Python which is a
  dynamically typed language, allowing freedom in using flexible length of
  arrays.
author: syncster
date: 2023-03-27T04:29:26.836Z
tags:
  - programming
---
A﻿side from pointers, this is also what confuses me back then when I was first learning C, the dynamic memory allocation. When I learned to program in Python, I wonder why would I ever go back to C with the limitation of the length of arrays to what length was declared to them.

## The Problem

In the problem below, I will declare an array of character (string) with fixed size and then try to concatenate to it with an additional string.

```c
#include <stdio.h>
#include <string.h>

int main() {
  char str1[19] = "The quick brown fox";
  char str2[] = " jumps over the lazy dog.\n";

  strcat(str1, str2);

  printf("%s\n", str1);

  return 0;
}
```

If we build this code using `gcc filename.c`, it will build with no compiler error or warning. However, if we run it, we will get a runtime error saying

```
trace trap
```

In C, a "Trace Trap" runtime error generally occurs when the program being executed encounters an unexpected error or exception that is not handled by the program. Specifically, a "Trace Trap" error occurs when the program encounters a trap instruction that was placed in the code for debugging purposes.

Traps are special instructions that can be used to interrupt the normal flow of a program and transfer control to a debugging routine or operating system. They are often used to catch errors or exceptions in code, and can be triggered by a variety of events such as a divide-by-zero error or an invalid memory access.

When a "Trace Trap" error occurs, it usually indicates a bug or programming error in the code, such as an uninitialized variable or an out-of-bounds array access. To fix the error, you will need to carefully examine the code and identify the root cause of the problem. Debugging tools like a debugger or printf statements can be helpful in this process.

## The Solution

To solve this issue, the following is a one way to go for a solution to this kind of problem. I will declare a pointer that will contain an initially allocation for length.

```c
char * str1 = (char*) malloc(sizeof(char) * 20);
```

The char data type has one (1) byte of size so this `str1` variable has been allocated 20 bytes.

The revised code will be

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main()
{
    char *str1 = (char *)malloc(sizeof(char) * 20);

    strcpy(str1, "The quick brown fox");

    char str2[] = " jumps over the lazy dog.";

    int total_length = strlen(str1) + strlen(str2);

    str1 = (char *)realloc(str1, sizeof(char) * total_length);

    strcat(str1, str2);

    printf("%s\n", str1);

    free(str1);

    return 0;
}
```

Here we use the library `stdlib` by `<stdlib.h>` to use the `free` function free up the memory used by `str1`.  If we do not free the memory, it will result in what is called a memory leak. 

Take note that this code could also work even if we don't use the `realloc` function to resize the `str1` but only sometimes and it is dangerous.