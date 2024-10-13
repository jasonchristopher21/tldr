---
sidebar_position: 8
---

# Week 9: Course Scheduling

:::info

Recommended to try past Practical Exam (also past PS5A) on [Kanna's Friendship](https://open.kattis.com/problems/kannafriendship). If you can do that, looking at this problem is now a piece of cake xD

:::

## Intuition

For this problem, we need to store who are enrolled to a course, and we need to **avoid duplicates**

:::tip
When we require storing certain objects with no duplicates, this should tell you that most likely we are handling cases which uses a **Set Data Structure**, and not a List data structure
:::

However, we also want the courses to be sorted alphabetically.

### Naive Solution: HashMap

So one solution we can think of is, what if we map each course to a set of students who are enrolled in the courses. Then we keep track of one `HashMap<String, HashSet<String>>`, saying that each course now maps to a hashset of names.

This is a plausible solution, however, in the end we need to sort the keys of the hashmap again to obtain an alphabetical ordering.

### Better Solution: TreeMap

:::tip
When you need hashmap to be in ordered, use TreeMap
:::

TreeMap is an ordered map, which orders the keys based on their natural ordering, or by specifying it. So we can just modify the naive solution from using a HashMap to using a TreeMap, and we're done!

## Algorithm

## Code

```java title="coursescheduling.java"
import java.util.*;
import java.io.*;

public class coursescheduling {
    public static void main(String[] args) throws IOException {

        // Ommitted: I/O

        int n = Integer.parseInt(br.readLine());

        // Initialise TreeMap
        TreeMap<String, HashSet<String>> map = new TreeMap<>();

        while (n-- > 0) {
            // Ommitted: I/O

            // Initialise a new HashSet, if course is not part of the map
            if (!map.containsKey(course)) {
                map.put(..., new HashSet<>());
            }

            // Add name to the hashset of that course
            map.get(...).add(...);
        }
        
        // Iterate through every key. This will iterate the keys of the map
        // in sorted order!
        for (String course : map.keySet()) {
            // Ommitted: Print output
        }

        pw.flush();
    }
}
```