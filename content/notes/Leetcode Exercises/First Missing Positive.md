# Question

Given an unsorted integer array `nums`. Return the _smallest positive integer_ that is _not present_ in `nums`

You must implement an algorithm that runs in `O(n)` time and uses `O(1)` auxiliary space

Example 1:

Input: `nums = [1,2,0]`
Output: `3`
Explanation: The numbers in the range `[1,2]` are all in the array

Example 2:

Input: `nums = [3,4,-1,1]`
Output: `2`
Explanation: `1` is in the array but `2` is missing

Example 3:

Input: `nums = [7,8,9,11,12]`
Output: `1`
Explanation: The smallest positive integer `1` is missing

# Solution

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (nums[i] > n || nums[i] <= 0) nums[i] = n+1;
        }

        for (int i = 0; i < n; i++) {
            int x = Math.abs(nums[i]);

            if (x > n) continue;
            x--;
            if (nums[x] > 0) nums[x] *= -1;
        }
        
        for (int i = 0; i < n; i++) {
            int x = nums[i];
            if (x > 0) return i+1;
        }

        return n+1;
    }
}
```


<mark style="background: #FFF3A3A6;">Case 1</mark>

If an array of size `n` is filled with all the numbers `1` to `n`, then the smallest integer not present in the array is `n+1`

<mark style="background: #FFF3A3A6;">Case 2</mark>

If an array does not contain all the numbers from `1` to `n`, since we are looking for the smallest **positive** *integer*, this means that the answer cannot be 0 or less, so we know `0 < x`. Since the array does not contain all numbers `1` to `n`, we know there is at least one value between `1` and `n`, this is our answer

<mark style="background: #FFB86CA6;">Algorithm</mark>

<mark style="background: #BBFABBA6;">First Walk Through</mark>

To find our answer, we first replace any numbers less than `0` or greater than `n` with the value `n+1`, we can ignore these numbers as they do not meet the conditions our answer needs, we replace them with the value `n+1` because of the first case we examined

<mark style="background: #BBFABBA6;">Second Walk Through</mark>

Now we look at the value in each array position, we take this value and mark the element at that position by making it negative. *We are using the index of the array to remember which numbers have already turned up, and are therefore not missing*

If a value is greater than `n`, we can ignore it as we know the only value greater than `n` that is significant, is `n+1`

We do `x--` as we are remembering what numbers have turned up using a *0 indexed* array

<mark style="background: #BBFABBA6;">Final Walk Through</mark>

Now we walk through the array one more time, once we come across the first index that we have not marked, we return that index as our answer

The final return statement is our first case where all the numbers `1` to `n` were found in the array, so every number in that array was negative by the end of the algorithm