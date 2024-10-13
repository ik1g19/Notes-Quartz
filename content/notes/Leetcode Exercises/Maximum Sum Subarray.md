Let's say you want to find the maximum sum of any subarray of size `k` in an array `nums`.

**Naive Approach**:

- Consider every subarray of size `k`, compute their sums, and find the maximum. This would take `O(n*k)` time.

**Sliding Window Approach**:

- Instead, use a sliding window:
    1. Start with the first `k` elements as the initial window.
    2. Move the window by one position to the right, adding the new element on the right and removing the element on the left.
    3. Keep track of the maximum sum seen so far.
    4. This approach only requires `O(n)` time.

### Code Example (Python):

```python
def max_sum_subarray(nums, k):
    n = len(nums)
    if n < k:
        return None

    # Calculate the sum of the first window
    max_sum = sum(nums[:k])
    current_sum = max_sum

    # Slide the window over the array
    for i in range(k, n):
        current_sum += nums[i] - nums[i - k]  # Slide the window to the right
        max_sum = max(max_sum, current_sum)   # Update max_sum if current_sum is greater

    return max_sum

# Example usage
nums = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(nums, k))  # Output: 9
```
