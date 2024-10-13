
#leetcode
# Question

Given an integer array `nums`, return `true` if there exists a triple of indices `(i, j, k)` such that `i < j < k` and `nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

Example 1:

Input: `nums = [1,2,3,4,5]`
Output: `true`
Explanation: Any triplet where `i < j < k` is valid.

Example 2:

Input: `nums = [5,4,3,2,1]`
Output: `false`
Explanation: No triplet exists.

Example 3:

Input: `nums = [2,1,5,0,4,6]`
Output: `true`
Explanation: The triplet `(3, 4, 5)` is valid because `nums[3] == 0 < nums[4] == 4 < nums[5] == 6`

# My Solution

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int n = nums.length;

        int a = Integer.MAX_VALUE;
        int b = Integer.MAX_VALUE;
        for (int i = 0; i<=n-3; i++) {
            if (nums[i] < a) {a = nums[i];}
            if (nums[i+1] > a && nums[i+1] < b) {b = nums[i+1];}
            if (nums[i+2] > b) {return true;}
        }

        return false;
    }
}
```

This walks the array and records the smallest number found so far `a`

It also records the smallest number found so far, that is greater than `a` - called `b`

If there is also a number to the right greater than `b`, then a triplet exists