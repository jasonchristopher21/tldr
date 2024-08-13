---
sidebar_position: 6
---

# Week 7B: Annoyed Coworkers

## Problem Statement

[open.kattis.com/problems/annoyedcoworkers](https://open.kattis.com/problems/annoyedcoworkers)

## Goal

Added demonstration on greedy choice property

## Intuition

Another greedy algorithm solution here, since "intuitively", you want to select those that potentially result in a lower annoyance level at every time.

Here, we can only sort based on two properties:
- Sorting based on increasing initial annoyance level
- Sorting based on increasing future annoyance level

By simulating with the example of if you have two coworkers, coworker 1 with initial annoyance of 1 and increment of 100, and coworker 2 with initial annoyance of 2 and increment of 3, and we want to annoy just 1 coworker.

After understanding the problem, we would pick coworker 2, because the future annoyance level would be 2 + 3, which is 5. Compared to picking coworker 1 which results to 101.

Hence, the greedy choice property would now be to pick coworkers **in ascending order of future annoyance level**

## Algorithm

- Have a Priority Queue that sorts coworkers based on **increasing future annoyance level**
- While we need to annoy some coworker:
  - Poll out the coworker with the least future annoyance level
  - Set the maximum future annoyance as `Math.max(current annoyance, this coworker's future annoyance)`
  - Insert coworker back to PQ, now with future annoyance level incremented by their change in annoyance

Code is ommitted, since this is yet another simple problem.