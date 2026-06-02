# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

**Difficulty :** Easy

## Topics / Patterns

* Dynamic Programming
* Fibonacci Sequence
* Pattern Recognition
* Memoization (conceptual)
* Mathematics

---

## Problem Statement

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps.

Return the number of distinct ways to climb to the top.

### Constraints

* `1 <= n <= 45`

---

## Examples

### Example 1

**Input**

```text
n = 2
```

**Output**

```text
2
```

**Explanation**

There are two ways to reach the top:

1. 1 step + 1 step
2. 2 steps

### Example 2

**Input**

```text
n = 3
```

**Output**

```text
3
```

**Explanation**

There are three ways to reach the top:

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

---

## My Understanding

My first thought was to solve this using Permutations and Combinations because I was trying to count all possible arrangements of 1-step and 2-step moves.

However, after writing out small cases manually, I noticed a pattern emerging:

```text
n = 1 → 1
n = 2 → 2
n = 3 → 3
n = 4 → 5
n = 5 → 8
```

Instead of calculating combinations directly, it became clear that each answer could be built from previously solved subproblems.

This shifted my thinking from counting arrangements to recognizing a Dynamic Programming pattern.

---

## Key Observation

To reach step `n`, the last move can only be:

* A 1-step jump from `n - 1`
* A 2-step jump from `n - 2`

Therefore:

```text
ways(n) = ways(n - 1) + ways(n - 2)
```

This is exactly the same recurrence relation as the Fibonacci sequence.

---

## Approach

### Pattern-Based DP Approach

1. If `n <= 2`, return `n`.
2. Store the number of ways for the previous two steps.
3. Iterate from step `3` to `n`.
4. Calculate the current number of ways as:

```text
current = previous1 + previous2
```

5. Shift the variables forward.
6. Return the final answer.

Since only the previous two values are needed, there is no need for an entire DP array.

---

## Dry Run

### Input

```text
n = 5
```

### Initial State

```text
a = 1
b = 2
```

| Step | Calculation | Result |
| ---- | ----------- | ------ |
| 3    | 1 + 2       | 3      |
| 4    | 2 + 3       | 5      |
| 5    | 3 + 5       | 8      |

### Final Answer

```text
8
```

There are 8 distinct ways to reach the 5th stair.

---

## Solution

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if(n <= 2) return n;

        int a = 1, b = 2;

        for(int i = 3; i <= n; i++) {
            int c = a + b;
            a = b;
            b = c;
        }

        return b;
    }
};
```

## Complexity Analysis

| Metric           | Complexity |
| ---------------- | ---------- |
| Time Complexity  | O(n)       |
| Space Complexity | O(1)       |

---

## Patterns Learned

* Dynamic Programming can often be reduced to storing only the necessary previous states.
* Many counting problems can be transformed into recurrence relations.
* Recognizing Fibonacci-like patterns can significantly simplify a problem.

---

## Similar Problems

* Fibonacci Number
* Min Cost Climbing Stairs
* N-th Tribonacci Number
* Count Ways To Build Good Strings
* Find Number of Ways to Reach the K-th Stair

---

## Revision Notes

* First instinct was Permutations & Combinations.
* Writing small cases manually revealed a pattern.
* The recurrence relation is:

```text
ways(n) = ways(n-1) + ways(n-2)
```

* This is essentially a Fibonacci sequence problem.
* Only the previous two values are required, allowing O(1) space.
* A common interview follow-up is converting the DP array solution into a space-optimized solution.
