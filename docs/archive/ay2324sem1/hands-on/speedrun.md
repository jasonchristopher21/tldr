---
sidebar_position: 5
---

# Week 7A: Speedrun

## Problem Statement

[open.kattis.com/problems/speedrun](https://open.kattis.com/problems/speedrun)

## Goal

This is a demonstration of a simple greedy-choice problem

## Intuition

For those of you who are familiar with greedy algorithms, looking at this will immediately ring a bell in your head: This is exactly just the interval scheduling problem!

For those who are not familiar, here's a quick guidethrough:
- $N$ has a bound of at most $10^5$. Hence, a $O(n^2)$ brute force solution cannot work here. Instead, we need to optimise further, and coming up with an $O(n log n)$ solution would work here
- As of the current week, all we know is two algorithms to give us the $O(n log n)$ solution, that is, either sorting or priority queue

How can we solve this by sorting?
- Greedy choice property: We take the best possible case at that point in time.

There are three options here that we can sort the intervals:
- Sort based on increasing start time
- Sort based on increasing end time
- Sort based on increasing interval length.

Let us examine the options:

### Sort based on increasing start time. 

Suppose that we want to sort based on increasing start time. However, if you have the following intervals: ${(0, 10), (1, 2), (3, 4), (5, 6), (7, 8)}$, The maximum number of non-overlapping intervals is 4, obtained from ${(1, 2), (3, 4), (5, 6), (7, 8)}$. However, if we take the smallest start time, then we will only have 1 interval which is $(0, 10)$. This is not an optimal solution indeed.

### Sort based on increasing length.

Suppose that we sort based on increasing length. If we have the intervals ${(0, 10), (12, 20), (9, 13)}$, by length we will choose $(9, 13)$ which gives us just one interval, but actually the largest set of non-overlapping intervals is indeed ${(0, 10), (12, 20)}$. This is not an optimal solution indeed

### Sort based on increasing end time.

Suppose we sort based on the increasing end time. This is in fact optimal, and can be proven by contradiction:
- Take two sets, one produced by the greedy set $G$ and one produced by the optimal set $OPT$
- Suppose that there exists an integer $r$ such that for the first $r - 1$ intervals chosen by the Greedy Set $G$ exactly matches the one chosen by the optimal set $OPT$.
- Hence, now we have the $r$-th job chosen by $G$ is different from that of $OPT$.
- If $OPT$ doesn't choose $G_r$, this implies that the end time of $OPT_r$ is greater than that of $G_r$.
- However, we can easily replace $OPT_r$ by $G_r$ in the optimal solution, and this will still remain the optimal solution, if not better.

Hence, we have proven that the increasing end time is a correct greedy choice property

## Algorithm

- Sort the intervals based on $t_{end}$
- Initialise a `count` variable to keep track of the length of the largest interval
- While there is an interval in the sorted range:
  - Take one interval as the current interval
  - Increment count by 1
  - Remove all intervals that overlap with the current interval
- If `count > G` (i.e. the maximum non-overlapping intervals is greater than the minimum number of tasks you need to do), print "YES". Else, print "NO".

Code is ommitted for this question, since this should not be a difficult problem to handle :)