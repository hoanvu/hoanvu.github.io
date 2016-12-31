---
layout: post
title: "Return multiple values from a C function"
date: 2017-01-01 00:02:00 +0700
categories: c_c++
tags: pointer 
---

Basically C allows you to return only a single value from a function, but if you know pointer, everything's changed. A small trick with this tool with let you return as many values as you want from a C function.

In this post, I'll show you that we can use pointer to return sum, difference, product and quotient of 2 numbers. Let's call this function **math()**, it has 2 numbers as input and return their sum. The difference, product and quotient will be stored in pointers to be retrieved later.

Let's get the function prototype:

```c
int math(int, int, int *, int *, float *);
```

First version looks like this:

```c
int math(int number1, int number2, int *difference, int *product, float *quotient) {
    // Get sum
    return number1 + number2;
}
```

As shown, the function already returned the sum of 2 input numbers. Next, we'll calculate the remaining mathematical operations. It's quite straightforward if you read about pointer.

```c
int math(int number1, int number2, int *difference, int *product, float *quotient) {
    // Perform subtraction, multiplication and division
    *difference = number1 - number2;
    *product = number1 * number2;
    *quotient = number1 / number2;

    // Get sum
    return number1 + number2;
}
```

As you see, this function only returns only one value as any other C function, but behind the scence, it already stored other values, each in a separate pointer to be retrieved later anytime we need.

So how to extract those values from the **math()** function?

In the main function, you can define a separate value for each pointer and pass them as references to the calling function:

```c
int main(int argc, char *argv[]) {
    int sum, diff, prod;
    float quo;

    sum = math(10, 2, &diff, &prod, &quo);

    printf("10 + 2 = %d \n", sum);
    printf("10 - 2 = %d \n", diff);
    printf("10 * 2 = %d \n", prod);
    printf("10 / 2 = %.2f \n", quo);

    return 0;
}
```

Output looks like this:

```bash
$ gcc -o math math.c
$ ./math 
10 + 2 = 12 
10 - 2 = 8 
10 * 2 = 20 
10 / 2 = 5.00
```