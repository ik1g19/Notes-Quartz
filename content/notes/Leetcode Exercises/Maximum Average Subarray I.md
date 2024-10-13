#java #leetcode
# Question

You are given an integer array `nums` consisting of `n` elements, and an integer `k`.

Find a contiguous subarray whose length is equal to `k` that has the maximum average value and return _this value_. Any answer with a calculation error less than `10-5` will be accepted.

Example 1:

Input: `nums = [1,12,-5,-6,50,3], k = 4`
Output: `12.75000`
Explanation: Maximum average is `(12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75`

Example 2:

Input: `nums = [5], k = 1`
Output: `5.00000`

# My Solution

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int sum = 0;
        for (int i = 0; i<k; i++) {
            sum += nums[i];
        }
        double avg = (double) sum / k;

        double maxAvg = avg;

        for (int i = k; i<nums.length; i++) {
            avg = avg - ((double) nums[i-k]/k) + ((double) nums[i]/k);

            maxAvg = Math.max(avg, maxAvg);
        }

        return maxAvg;
    }
}
```

This uses a sliding window to recalculate the average

The averages changes by `-Element leaving window/k` and `+Element entering window/k`