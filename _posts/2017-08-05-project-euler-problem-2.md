---
layout: post
title: "Project Euler - Problem 2"
date: 2017-08-05 11:54:00 +0700
categories: project_euler
tags: euler sum_even_fibonacci
---

<strong>Link:</strong> https://projecteuler.net/problem=2

<strong>Problem details:</strong>

```
Each new term in the Fibonacci sequence is generated by adding the previous two terms. By starting with 1 and 2, the first 10 terms will be:

1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

By considering the terms in the Fibonacci sequence whose values do not exceed four million, find the sum of the even-valued terms.
```

This is also a fairly simple problem. The first solution that comes to anyone's mind is to calculate the Fibonacci number and then check whether it's an even number, if so add it to the cumulative sum:

```
1. Calculate the next Fibonacci number
2. Is this number divisible by 2
    2.1. If yes, add it to the result
    2.2. Else, calculate the next number
3. Return the sum
```

This should be fine for most cases, but we will need to check each and every number in the series whether they are an even number or not. So we can improve it. Looking closely at a Fibonacci series, we can see that every third Fibonacci number is an even number (in this problem, the first even number is 2, which lies in the second position):

```
Series:     1 - 2 - 3 - 5 - 8 - 13 - 21 - 34 - 55 - 89 - 134 ...
Position:   1 - 2 - 3 - 4 - 5 - 6  - 7  - 8  - 9  - 10 - 11  ...
```

So, we don't need to check if a Fibonacci number is an even number or not, all we need to do is to keep track of the third Fibonacci number, and just add it to the sum. This can save lots of checking operation if the Fibonacci series is big.

Here's the source code in Python for your reference:

```python
# Initialize the first 2 numbers in the series
first = 1
second = 2
# Sum of even Fibbonaci numbers, so sum will be initialized to the first even number "second"
sum_even_fib = second
# Get the third number
third = first + second

while third <= 4000000:
    first = second + third
    second = first + third
    third = first + second

    # We need to keep track of the third Fibonacci number from the first even number in the series,
    # which is 2 (in second position)
    sum_even_fib += second

print(sum_even_fib)
```

On Github: [https://github.com/hoanvu/project_euler/blob/master/problem_002.py](https://github.com/hoanvu/project_euler/blob/master/problem_002.py) 