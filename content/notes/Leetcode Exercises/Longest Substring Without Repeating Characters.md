#leetcode 

# Question

Given a string s, find the length of the longest
substring
without repeating characters.


Example 1

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring

# My Answer


```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        strLength = len(s)

        charSet = set()
        left = 0
        maxLength = 0

        for right in range(strLength):
            while s[right] in charSet:
                charSet.remove(s[left])
                left += 1
            charSet.add(s[right])
            maxLength = max(maxLength, right - left + 1)

        return maxLength
```

Maintain a `left` and `right` pointer

`right` iterates through the string

Maintain a `set` that keeps track of letters that have turned up so far

While a letter turns up that has already appeared, move the `left` pointer along and remove the character from the set