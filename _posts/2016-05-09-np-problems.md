---
layout: post
title: "NP Problems"
date: 2016-05-09 11:58:20 +0700
categories: algorithm
tags: algorithm np
---

Recently I was asked to research something called **NP problem**. NP stands for **Non-deterministic Polynomial** time. In simple term, it's a category of algorithms that we can not calculate its run time (in regular computer). So you may wonder what is **polynomial time**? It's the opposite, it's the class of algorithms that we can calculate its runtime based on the input size.

Have you ever heard of the term **Big O Notation**? If the answer is no, it's some kind of measurement people use to evaluate the speed an algorithm. For example, your boss gives you a list of numbers and asks you to write an algorithm to search for the minimum number in that list so she does not have to do it manually. A simple way to do this is to compare each pair of numbers in that list and keep track of the minimum number as you goes on. When you finishing iterating through every number, you now have the result to report back to your boss.

Now you may wonder how long does your algorithm run? Is it fast enough to satisfy her? Suppose she gave you **n** numbers. Every time the algorithm runs, it needs to check every items to make sure that the right number is returned. So we can say that the runtime of the algorithm is n. Now, this can be simply written as O(n). O is the short version of _Big O Notation_. So when your grumpy boss looks at this, she knows that if she gave your algorithm the input of 100 items, it takes 100 operations in order to get the result she needs.

So, **searching for some item in a list** can be classified as a **P** problem because its execution time can be measured by some function of input size. In other words, its runtime is polynomial.

Unfortunately, not every problem run in polynomial time, at least on regular computer, which means their runtime can not be determined using a linear function of the input size.

Some examples of NP problems are:

+ Greedy algorithm
+ Knapsack problem
+ Travelling Salesman problem
+ ...

There is a [million dollar question](https://en.wikipedia.org/wiki/Millennium_Prize_Problems) that if anybody can prove that "N=NP", that person will be granted a million dollar from Clay Mathematics Institute. 