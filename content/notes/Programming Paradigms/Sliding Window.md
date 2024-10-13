The basic idea is to maintain a window (a subrange) over a sequence and "slide" this window to cover different parts of the sequence, usually in one pass, to solve a problem without having to recompute results for overlapping subranges.

### How the Sliding Window Algorithm Works

1. **Fixed-size Window**:
    
    - In a fixed-size sliding window, the window's size remains constant as it moves across the sequence. This is often used when you're looking for subarrays or substrings of a specific length.
    - Example: Finding the maximum sum of a subarray of length `k` in an array.
2. **Variable-size Window**:
    
    - In a variable-size sliding window, the window's size can change dynamically based on certain conditions. This is useful in problems where the window should expand or contract based on some criteria.
    - Example: Finding the smallest subarray with a sum greater than or equal to a target value.

### Example Problem

[[notes/Leetcode Exercises/Maximum Sum Subarray|Maximum Sum Subarray]]

