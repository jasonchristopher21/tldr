---
sidebar_position: 7
---

# Week 8: Accounting (/bokforing)

## Problem Statement

[open.kattis.com/problems/bokforing](https://open.kattis.com/problems/bokforing)

## Goal

Seems like a simple hashing problem, but `RESTART` operations are pain in the @$$

## Intuition

It is simple to come up with the naive solution of setting each item directly to a data structure. And in fact, that works ... well until `RESTART` appears.

### Problem with modifying each account upon `RESTART`

If we have to modify the entries of the bank accounts on every `RESTART` operation, then we would end up with an $O(n)$ algorithm for every `RESTART` query. Too slow.

### How to modify `RESTART`

If we want to reduce it from $O(n)$, most likely it will either come down to $O(\log n)$ or $O(1)$. This will scope down what operations we can do.

- Can we do $O(\log n)$? Seems impossible: we don't need binary search, nor can't we use a priority queue - equivalent for this question
- Can we do in $O(1)$?

To solve this in $O(1)$ time, we need to observe that initially all the wealth is set to $0. Hence, if we can somehow manage to utilise this item, we can do RESTART by just modifying the initial wealth.

## Algorithm

Now, whenever we do RESTART, this is what we do:
- Set the initial wealth as the RESTART value
- **Clear the entire hash table**

Hence, whenever we call get:
- If the value is not in the hash table (either the bank account is not there, or has been restarted), then we return simply the initial value
- If the value is there (most likely the bank account has been set after a restart operation), then we return the entry.

## Code

Ommitted to adjust with non-AC solution.

```java title="bokforing.java"
public class bokforing {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter pw = new PrintWriter(System.out);
        
        // initialise hashmap
        HashMap<Integer, Integer> map = new HashMap<>();

        //highlight-start
        // initialise an intiial wealth value (the restarted value)
        int lastRestart = 0;
        //highlight-end
        
        String[] firstLine = br.readLine().split(" ");
        int n = Integer.parseInt(firstLine[0]);
        int q = Integer.parseInt(firstLine[1]);

        while (--q >= 0) {
            String[] line = br.readLine().split(" ");
            if (line[0].equals("PRINT")) {
                // If the index is not in the hashmap, return lastRestart.
                // Else, return the netry in the hashmap
                int idx = Integer.parseInt(line[1]);
                if (map.containsKey(idx)) {
                    pw.println(...);
                } else {
                    pw.println(...);
                }
            }
            if (line[0].equals("RESTART")) {
                // Set lastRestart to the new value
                lastRestart = ...;
            }
            if (line[0].equals("SET")) {
                // Just put to the hashmap
                map.put(..., ...);
            }
        }
        pw.flush();
    }
}

```