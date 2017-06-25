---
layout: post
title: "Project Euler - Problem 1"
date: 2017-06-25 21:00:00 +0700
categories: project_euler
tags: euler sum_divisible_by_3_and_5 
---

<strong>Link:</strong> https://projecteuler.net/problem=1

<strong>Problem details:</strong>

```
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Find the sum of all the multiples of 3 or 5 below 1000.
```

This is a fairly simple problem. At first look we can use brute force by scanning from 1 to 999 and find all number that are either divisible by 3 or 5 and add them together. An implementation in Python would be:

```python
sum = 0
for i in range(1, 1000):
    if i % 3 == 0 or i % 5 == 0:
       sum += i
    
print sum # 233618
```

But let's say the upper bound is not 1000, but a big number like few billions, this algorithm would be very slow. Its performance is O(n).

Another better approach would be to understand the nature of the input. Let's analyze the sum of all multiples of 3:

```
sum = 3 + 6 + 9 + 12 + ...
```

Then:

```
sum = 3 * (1 + 2 + 3 + 4 + ...)
=> sum = 3 * ( (n + 1) / 2 )  # n is the amount of numbers that are multiples of 3
```

This will greatly improve the speed of our program because in theory it only needs to perform O(1) to get the sum (never be O(1) practically). Now how do we find the numbers of multiples of 3 under some upper bound?

```
- Under 9 there are 2 multiples of 3: 3 and 6                   # (9 - 1) / 3
- Under 10 there are 3 multiples of 3: 3, 6 and 9               # (10 - 1) / 3
- Under 15 there are 4 multiples of 3: 3, 6, 9 and 12           # (15 - 1) / 3
- Under 20 there are 6 multiples of 3: 3, 6, 9, 12, 15 and 18   # (20 - 1) / 3

=> the general formula is: (upper_bound - 1) / 3
```

Similarly, we can get the exact analysis for all multiples of 5. 

Our algorithm looks like below in Python:

```python
from __future__ import division

MAX_VALUE = 1000

def sumDivisibleBy(n):
    # Get the amount of numbers that are multiples of n
    p = (MAX_VALUE - 1) // n
    
    return ( n * p * (p + 1) ) / 2

# Now get the sum of all multiples of 3 and 5
print sumDivisibleBy(3) + sumDivisibleBy(5)     # 266333.0
```

Wait, the result is <strong>266333.0</strong>, which is bigger than the expected result. The reason is because with this approach, numbers that are multiples of both 3 and 5 (like 15, 30, ...) will be calculated twice, so we need to exclude them from the result:

```python
print sumDivisibleBy(3) + sumDivisibleBy(5) - sumDivisibleBy(15)    # 233168 - Good!
```

Now we get the correct sum!