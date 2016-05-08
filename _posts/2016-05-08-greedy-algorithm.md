---
layout: post
title: "Greedy Algorithm"
date: 2016-05-08 11:58:20 +0700
categories: algorithm
tags: algorithm greedy np
---

Recently I was asked to research something called **NP problem**. NP stands for **Non-deterministic Polynomial** time. In simple term, it's a category of algorithms that we can not calculate its run time (in regular computer). So you may wonder what is **polynomial time**?

Have you ever heard of the term **Big O Notation**? If the answer is no, it's some kind of measurement people use to evaluate the speed an algorithm. For example, your boss gives you a list of numbers and asks you to write an algorithm to search for the minimum number in that list so she does not have to do it manually. A simple way to do this is to compare each pair of numbers in that list and keep track of the minimum number as you goes on. When you finishing iterating through every number, you now have the result to report back to your boss.

Now you may wonder how long does your algorithm run? Is it fast enough to satisfy her? Suppose she gave you **n** numbers. Every time the algorithm runs, it needs to check every items to make sure that the right number is returned. So we can say that the runtime of the algorithm is n. Now, this can be simply written as O(n). O is the short version of _Big O Notation_. So when your grumpy boss looks at this, she knows that if she gave your algorithm the input of 100 items, it takes 100 operations in order to get the result she needs.

Unfortunately, not every problem 