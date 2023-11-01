---
sidebar_position: 2
---

# Week 4: Basic Programming 2

## Problem Statement

[open.kattis.com/problems/basicprogramming2](https://open.kattis.com/problems/basicprogramming2)

## Goal

This is the second problem, which basically addresses the concepts that are taught in Week 4's tutorial about the applications of binary search.

## Intuition

### Step 1: x + y = 7777

One look at this question and you will realise that this is basically the [two-sum](https://leetcode.com/problems/two-sum/) problem like the popular LeetCode problem.

To solve for this, we can utilise the method that was taught in class, that is the **two-pointer** method:

1. Intialise to pointers, a `start` pointer and an `end` pointer
2. Sort the array
3. While the start pointer and the end pointer do not meet (`while start != end`):
    1. Check if `Array[start]` is equal to `Array[end]`
    2. If they are equal, we have found a pair (start, end).
    3. If not, then we check the sum:
        1. If the sum is less than 7777, then we have to increase the sum. That is, we shift the start pointer to the right
        2. If the sum is greater than 7777, then we have to lower the sum. That is, we shift the end pointer to the left.

The following code gives us the intuition of two-sum in Java:

```java
int[] numbers = new int[N];
for (int i = 0; i < N; i++) {
    numbers[i] = i; // modify the numbers array here!
}

// two-sum logic

// Sort the numbers array
Arrays.sort(numbers);

// Initialise start and end pointers
int start = 0;
int end = N - 1;

boolean found = false;

// Iterate:
while (start != end) {
    int sum = numbers[start] + numbers[end];
    
    // if sum is 7777, we found the solution
    if (sum == 7777) {
        found = true;
        break;
    } 

    // If sum is less than 7777, increase the start pointer
    if (sum < 7777) {
        start++;
    }

    // If sum is greater than 7777, decrease the end pointer
    if (sum > 7777) {
        end--;
    }
}
```

:::tip
If a similar problem happen to appear, there is actually a better method that reduces the time complexity from $O(n \log n)$ to $O(n)$. This method does not use sorting.

So we can actually use a HashMap to solve the two-sum problem. This LeetCode solution link would help in describing how the HashMap can be used:

[https://leetcode.com/problems/two-sum/solutions/3619262/3-method-s-c-java-python-beginner-friendly/](https://leetcode.com/problems/two-sum/solutions/3619262/3-method-s-c-java-python-beginner-friendly/)

:::

### Step 2: Check for Uniqueness

To check for uniqueness, we can do the following:

- Sort the numbers array
- Compare each item to the item after that
  - If the item in index $i$ is equal to the item in index $i+1$, then the array contains duplicates

:::info

Why does this work? Since we are sorting the array, we are confident that if a duplicate item exist, then they would be next to each other, otherwise it breaks the sorted property.

This reduces the time complexity of our solution from $O(n^2)$ (brute-force solution) to $O(n \log n)$ (because of sorting)

:::

```java
boolean unique = true;
Arrays.sort(numbers);
for (int i = 0; i < N - 1; i++) {
    if (numbers[i] == numbers[i + 1]) {
        unique = false;
        break;
    }
}
if (unique)
    pw.println("Unique");
else
    pw.println("Contains Duplicate");
```

:::tip

Now that we learn hashing, we can also reduce this to a $O(n)$ complexity. To do that, we can simply create a `HashSet`, then for every item, we check if the item is part of the HashSet or not. 

- If it is, then we know that there are duplicates.
- If it is not in the HashSet, then we add the item to the HashSet

An alternative approach:

- For each integer, add the integer into the HashSet
- Check if the size of the hashset is equal to the array size. If it is equal, then it is unique.


```java
HashSet<Integer> set = new HashSet<>();
for (int num : numbers) {
    set.add(num);
}
if (set.size() == numbers.length) {
    pw.println("Unique");
} else {
    pw.println("Contains duplicates");
}
```
:::

### Step 3: Finding Majority Item

A sorting approach to this question would be:

- Sort the array of numbers
- Keep track of a variable that stores the previous number, and the running count.
- Iterate through the array of numbers:
  - If the number is equal to the previous number, increment the count
  - If it is not equal, then:
    - Set previous number as the current number
    - Reset count to 1
  - Check if count is greater than $N/2$. If it is, then we have found the majority item.

```java
Arrays.sort(numbers);
    int count = 1;
    int currentNumber = numbers[0];
    boolean found = false;
    for (int i = 1; i < N; i++) {
        if (numbers[i] == currentNumber) {
            count++;
        }
        else {
            count = 1;
            currentNumber = numbers[i];
        }
        if (count > N / 2) {
            pw.println(currentNumber);
            found = true;
            break;
        }
    }
    if (!found)
        pw.println(-1);
```

:::info

For fun, here's an interesting algorithm you can look at! (Non-examinable, non-tested, non-trivial. Just open if you are interested / kaypoh)

[Moore's Voting Algorithm](https://www.geeksforgeeks.org/boyer-moore-majority-voting-algorithm/)

:::

### Step 4: Print Median integer

This should be quite straightforward. Basically,

- Sort the array of numbers
- If it is odd, then return the middle number
- If it is not, take the average of the two middle numbers

```java
Arrays.sort(numbers);
if (N % 2 == 0) {
    pw.println(numbers[N / 2 - 1] + " " + numbers[N / 2]);
}
else {
    pw.println(numbers[N / 2]);
}
```

:::tip
This can be improved by using QuickSelect, which has an expected $O(n)$ runtime.

Suppose if you meet problems which require you to _dynamically_ find the median, then a new data structure might be needed. One such data structure I can think of is having a bBST (probly an AVL tree). 

- Insertions and deletions are done in $O(\log n)$ time
- Finding the median is now reduced to $O(\log n)$ time
  - We only need to search for the $n/2$ element (if $n$ is odd) or the $n/2$ and $n/2 + 1$ element (if $n$ is even).
  - searching for an element in a bBST is $O(\log n)$. Worst case is if $n$ is even, then we have to make two calls.
  - Hence, complexity of finding the median is still $O(\log n)$

Therefore, if we have $Q$ queries consisting of both insertions and finding the median, then we have a runtime of $O(Q\log N)$. This is way better than $O(QN\log N)$ by sorting, or $O(QN)$ by QuickSelect.

Note, the above are worst case runtimes, not amortised yet.
:::

### Step 5: Print 

### Problem with `cut` and `leave`

Suppose the queue is `a b c d e`, then you want to execute `cut f b`. Then, all positions from `b` to `e` must be shifted to the right!

Same goes with if you have `a b c d e`, then you want to execute `leave a`. Then, all positions from `b` to `e` must be shifted to the left.

## Solution

To mitigate this, there are two ways we can do:

### Sol 1: Manual array shift

If we know the maximum size of the array needed, then we can simply create a static array, and implement our shift manually. 

This is a quick _uncompleted_ code that covers the case of `cut`:

```java title="cutinline.java"
import java.util.*;
import java.io.*;

public class cutinline {
    public static void main(String[] args) throws IOException {
        // Setup I/O methods
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter pw = new PrintWriter(System.out);

        // Setup line for queueing. Note that 0 <= N <= 1000 and 0 <= C <= 1000,
        // so we can safely set the size of the array to 2000.
        String[] line = new String[2000];
        int lastPersonIndex = 0;

        // Setup the initial line
        int N = Integer.parseInt(br.readLine());
        for (int i = 0; i < N; i++) {
            line[i] = br.readLine();
            lastPersonIndex++;
        }

        // Perform Commands
        int C = Integer.parseInt(br.readLine());

        while (C-- > 0) {
            String[] command = br.readLine().split(" ");

            // Cut command
            if (command[0].equals("cut")) {
                String cutter = command[1];
                String poorGuy = command[2];
                
                int personPointer = 0;

                // Find where the poor guy is located
                for (String person : line) {
                    if (person.equals(poorGuy)) {
                        break;
                    }
                    personPointer++;
                }

                // Shift everyone after poor guy by one position
                for (int i = lastPersonIndex; i >= personPointer; i--) {
                    line[i + 1] = line[i];
                }

                // Place the cutter in the poor guy's position
                line[personPointer] = cutter;
                lastPersonIndex++;
            }
        }

        // Print the final line
        for (int i = 0; i < lastPersonIndex; i++) {
            pw.println(line[i]);
        }
        
        pw.flush();
        br.close();
    }
}
```

### Sol 2: Dynamic Arrays

Instead of manually shifting the items around, what if we can just use a Java default implementation?

Let us use ArrayList instead!

<iframe src="https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html" width="720" height="360" />

The below shows how the _uncompleted_ code would look like using the ArrayList instead of manual shifting


```java title="cutinline.java"
import java.util.*;
import java.io.*;

public class cutinline {
    public static void main(String[] args) throws IOException {
        // Setup I/O methods
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter pw = new PrintWriter(System.out);

        // Setup the queue using ArrayList
        // highlight-start
        ArrayList<String> line = new ArrayList<>();
        // highlight-end

        // Setup the initial line
        int N = Integer.parseInt(br.readLine());
        for (int i = 0; i < N; i++) {
            // highlight-start
            line.add(br.readLine());
            // highlight-end
        }

        // Perform Commands
        int C = Integer.parseInt(br.readLine());

        while (C-- > 0) {
            String[] command = br.readLine().split(" ");

            // Cut command
            if (command[0].equals("cut")) {
                String cutter = command[1];
                String poorGuy = command[2];
                
                // Find where the poor guy is located
                // highlight-start
                int position = line.indexOf(poorGuy);
                // highlight-end

                // Place the cutter in the poor guy's position
                // highlight-start
                line.add(position, cutter);
                // highlight-end
            }
        }

        // Print the final line
        for (String person : line) { // we can use this instead of an index :)
            pw.println(person);
        }
        
        pw.flush();
        br.close();
    }
}
```

### Sol 3: Linked Lists

A bit overkill :") but will be seen in the `/joinstrings` hands-on problem