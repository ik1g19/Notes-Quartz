#leetcode #dynamic-programming

# Question

You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return _the minimum cost to reach the top of the floor_.

**Example 1:**

**Input:** cost = [10,15,20]
**Output:** 15
**Explanation:** You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.

**Example 2:**

**Input:** cost = [1,100,1,1,1,100,1,1,100,1]
**Output:** 6
**Explanation:** You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.

# Solution

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        return Math.min(minCost(cost, n-1), minCost(cost, n-2));
    }

    private int minCost(int[] cost, int n) {
        if (n<0) {return 0;}
        else if (n==0 || n==1) {return cost[n];}
        return cost[n] + Math.min(minCost(cost, n-1), minCost(cost, n-2));
    }
}
```

The recurrence relation between subproblems here is that the minimum cost of getting to the current stair, is the smaller of the minimum cost to get to either 1 or 2 stairs behind

```java
mincost(i) = cost[i]+min(mincost(i-1), mincost(i-2))

//Base cases:  
mincost(0) = cost[0]
mincost(1) = cost[1]
```

This initial approach has exponential time complexity since the cost for the same step will be recalculated multiple times

## Top Down

This approach uses top down dynamic programming to simply store the result of each calculation

```java
// Top Down Memoization - O(n) 1ms
int[] dp;
public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
    dp = new int[n];
    return Math.min(minCost(cost, n-1), minCost(cost, n-2));
}
private int minCost(int[] cost, int n) {
    if (n < 0) return 0; // Base case: beyond the first step
    if (n == 0 || n == 1) return cost[n];// Base case: first or second step
    
    // Memoization check: if already computed, return the cached result
    if (dp[n] != 0) return dp[n]; 
    
    // Recursive step
    dp[n] = cost[n] + Math.min(minCost(cost, n-1), minCost(cost, n-2));
    
    return dp[n];
}
```

## Bottom Up

This approach is bottom up since it starts from the base cases and iterates through subsequent steps 

```java
// Bottom up tabulation - O(n) 1ms
public int minCostClimbingStairs(int[] cost) {
	int n = cost.length;
	int[] dp = new int[n];
	for (int i=0; i<n; i++) {
		if (i<2) dp[i] = cost[i];
		else dp[i] = cost[i] + Math.min(dp[i-1], dp[i-2]);
	}
	return Math.min(dp[n-1], dp[n-2]);
}
```

