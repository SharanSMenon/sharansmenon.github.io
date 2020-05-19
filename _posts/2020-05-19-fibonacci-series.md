---
title: "Fibonacci Series in Python"
published: false
---

This post will cover a few different algorithms for the fibonacci series. Some are faster than others while some are slower than others.

## What is the fibonacci series?

The fibonacci series is a series of numbers where the next number is the result of the sum of the previous 2 numbers. The first two numbers of the series are 0 and 1.

The next number is the sum of 0 and 1 which is 1. The number after that is $1 + 1 = 2$. Like that, it keeps on going and going. Here are the first few numbers of the series:

0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, and so on...

## Recursive method

This is by far, the slowest and the most naive method. On my computer, it takes around 5 seconds to calculate the 35th fibonacci number. But calculating the first 10 numbers, it is actually faster than the other algorithms. But keep in mind, it is incredibly slow otherwise.

The idea behind this algorithm is really simple. Say we want to calculate the 5th fibonacci number. We calculate the sum of the numbers.
