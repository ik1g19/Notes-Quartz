#leetcode #dynamic-programming 

# Question

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = \[1,2,3,4]
**Output:** \[24,12,8,6]

**Example 2:**

**Input:** nums = \[-1,1,0,-3,3]
**Output:** \[0,0,9,0,0]

# My Solution

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;

        int[] ans = new int[n];

        int[] dp = new int[n];
        int[] dp2 = new int[n];

        dp[0] = 1;
        dp2[n-1] = 1;

        for (int i = 1; i<n; i++) {
            dp[i] = dp[i-1] * nums[i-1];
        }

        for (int i = n-2; i>=0; i--) {
            dp2[i] = dp2[i+1] * nums[i+1];
        }

        ans[0] = dp2[0];
        ans[n-1] = dp[n-1];

        for (int i = 1; i<n; i++) {
            ans[i] = dp[i] * dp2[i];
        }

        return ans;

    }
}
```

`dp[]` holds the cumulative product on the left hand side of where we are currently at whilst iterating through the array

`dp2[]` holds the cumulative product on the right hand side of where we are currently at whilst iterating through the array

# Space Optimised Solution

The following Solution stores the results directly into the answer array to optimise space

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int ans[] = new int[n];
        Arrays.fill(ans, 1);
        int curr = 1;
        for(int i = 0; i < n; i++) {
            ans[i] *= curr;
            curr *= nums[i];
        }
        curr = 1;
        for(int i = n - 1; i >= 0; i--) {
            ans[i] *= curr;
            curr *= nums[i];
        }
        return ans;
    }
}
```