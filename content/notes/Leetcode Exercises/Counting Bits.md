#leetcode

# Question

Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (`0 <= i <= n`), `ans[i]` is the **number of** `1`'s in the binary representation of `i`.

**Example 1:**

**Input:** n = 2
**Output:** \[0,1,1\]
**Explanation:**
0 --> 0
1 --> 1
2 --> 10

**Example 2:**

**Input:** n = 5
**Output:** \[0,1,1,2,1,2\]
**Explanation:**
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101

# Solution

```java
class Solution {
    public int[] countBits(int n) {
        int[] ans = new int[n+1];
        for (int i = 0; i <= n; i++) {
            ans[i] = ans[i >> 1] + (i & 1);
        }
        return ans;
    }
}
```

This uses a bit shifting (>>) dynamic programming approach to count the number of 1's in each binary number

Imagine taking the rightmost digit off a binary number, this is bit shifting everything to the right by 1, which has the same effect as halving the number

Therefore, the number of 1's in a binary number **n** can be thought of as the number of 1's **n/2**, in addition to possibly the extra 1 which was knocked off as the rightmost digit

The bitwise operation `&` can be used to find out if the rightmost binary digit is a 1: `i & 1`

The following loop counts the number of 1's in the number and stores it to be access at later points in the loop:

```java
for (int i = 0; i <= n; i++) {
	ans[i] = ans[i >> 1] + (i & 1);
}
```

