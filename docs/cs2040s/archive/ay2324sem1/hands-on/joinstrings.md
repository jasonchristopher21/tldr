---
sidebar_position: 3
---

# Week 5: Join Strings

## Problem Statement

[open.kattis.com/problems/joinstrings](https://open.kattis.com/problems/joinstrings)

## Goal

This is a demonstration of how to apply a linked list data structure to our solution.

## Intuition

It seems as a simple problem, but then we realise that string concatenation in Java is $O(n^2)$, which is considerably slow. This solution would _definitely_ TLE

### Problem with `StringBuilder`

As we have learned, `StringBuilder` reduces the time to concatenate strings from $O(n^2)$ down to $O(1)$, since appending strings will now take $O(1)$ time, and converting the `StringBuilder` object to a string takes $O(n)$ time to traverse.

Yet it seems that if we call `toString`, it might be too slow. 

## Idea

Hence, the idea here would be: what if we can print out the entire order of the string, without having to combine the strings together? What if we can somehow maintain some order without having to perform string concatenation

### Linked List solution

To solve this problem, we can keep track of the strings as nodes, then we connect one node to another through a Linked List data structure. To do that, we need to initialise:

- A Node that keeps track of the string value and a pointer to the next node
- An array that stores a mapping from the index to the pointer containing the string node
- The head of the string

Hence, the algorithm would be as follows:

- Every time we see a join operation, suppose we want to join string at index $a$ and index $b$. 
  - Access the Node of $a$ through the array
  - Set the `next` pointer of $a$ as $b$
  - Set the head of the string as a pointer to $a$

However, the catch is, **we should not concatenate the string anymore**, i.e. do not execute any call to do toString. Instead, **traverse the list and do `pw.print` on the go!**

### Java Implementation

Ommitted, non-AC solution (but with the LinkedList implementation):

```java title="joinstrings.java"

public class joinstrings {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter pw = new PrintWriter(System.out);

        int N = Integer.parseInt(br.readLine());

        // Set an array of string linked lists
        StringNodeList[] strings = new StringNodeList[N];
        
        // I/O ommitted

        int storeLastIndex = 0;

        while (--N > 0) {
            // Perform I/O to obtain a and b
            // Add node at strings[b - 1] after strings[a - 1]
            strings[a - 1].add(strings[b - 1]);

            // set store last index
            storeLastIndex = a - 1;
        }
        
        // Ommitted: Traverse the linked list and perform pw.print

        pw.flush();
        br.close();
    }
}

class StringNodeList {
    StringNode head;
    StringNode tail;

    public StringNodeList() {
        this.head = null;
        this.tail = null;
    }           

    public void add(StringNode node) {
        if (this.head == null) {
            this.head = node;
            this.tail = node;
        }
        else {
            this.tail.setNext(node);
            this.tail = node;
        }
    }

    public void add(StringNodeList list) {
        if (this.head == null) {
            this.head = list.head;
            this.tail = list.tail;
        }
        else {
            this.tail.setNext(list.head);
            this.tail = list.tail;
        }
    }
}

class StringNode {
    String value;
    StringNode next;

    public StringNode(String value) {
        this.value = value;
    }

    public StringNode(String value, StringNode next) {
        this.value = value;
        this.next = next;
    }

    public StringNode getNext() {
        return this.next;
    }

    public void setNext(StringNode next) {
        this.next = next;
    }
}
```
