#leetcode #dynamic-programming

# Question

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

**Example 1:**

**Input:** nums = \[1,2,3,1]
**Output:** 4
**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

**Example 2:**

**Input:** nums = \[2,7,9,3,1]
**Output:** 12
**Explanation:** Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12

# Solution

## General Approach to Solving Dynamic Programming Problems

This particular problem and most of others can be approached using the following sequence:

1. Find recursive relation
2. Recursive (top-down)
3. Recursive + memo (top-down)
4. Iterative + memo (bottom-up)
5. Iterative + N variables (bottom-up)

## Recursive Solution

A robber has 2 options: a) rob current house `i`; b) don't rob current house.  
If an option "a" is selected it means she can't rob previous `i-1` house but can safely proceed to the one before previous `i-2` and gets all cumulative loot that follows.  
If an option "b" is selected the robber gets all the possible loot from robbery of `i-1` and all the following buildings.  
So it boils down to calculating what is more profitable:

- robbery of current house + loot from houses before the previous
- loot from the previous house robbery and any loot captured before that

`rob(i) = Math.max( rob(i - 2) + currentHouseValue, rob(i - 1) )`

```java
class Solution {
    public int rob(int[] nums) {
        return maxRob(nums, nums.length-1);
    }

    private int maxRob(int[] nums, int i) {
        if (i<0) {return 0;}
        return Math.max(nums[i] + maxRob(nums,i-2), maxRob(nums,i-1));
    }
}
```

## Recursive and Memoized (Top Down)

```java
int[] memo;
public int rob(int[] nums) {
    memo = new int[nums.length + 1];
    Arrays.fill(memo, -1);
    return rob(nums, nums.length - 1);
}

private int rob(int[] nums, int i) {
    if (i < 0) {
        return 0;
    }
    if (memo[i] >= 0) {
        return memo[i];
    }
    memo[i] = Math.max(rob(nums, i - 2) + nums[i], rob(nums, i - 1));
    return result;
}
```

The same approach as before but uses an array to remember repeated calculations

## Iterative and Memoized (Bottom Up)

```java
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    int[] memo = new int[nums.length + 1];
    memo[0] = 0;
    memo[1] = nums[0];
    for (int i = 1; i < nums.length; i++) {
        int val = nums[i];
        memo[i+1] = Math.max(memo[i], memo[i-1] + val);
    }
    return memo[nums.length];
}
```

This iterates from the base cases upwards through the subsequent problems