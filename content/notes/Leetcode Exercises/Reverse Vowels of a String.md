#leetcode

# Question

Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`, and they can appear in both lower and upper cases, more than once.

Example 1:

Input: `s = "IceCreAm"`

Output: `"AceCreIm"`

Explanation:

The vowels in `s` are `['I', 'e', 'e', 'A']`. On reversing the vowels, s becomes `"AceCreIm"`.

Example 2:

Input: `s = "leetcode"`

Output: `"leotcede"`

# Solution

```java
class Solution {
    public String reverseVowels(String s) {
        String vowels = "aeiouAEIOU";
        char[] chars = s.toCharArray();

        int start = 0;
        int end = s.length()-1;

		//iterate through string with 2 pointers
        while (start < end) {
	        //if current char is in the vowels string
            while (start < end && vowels.indexOf(chars[start]) == -1) {
                start++;
            }

			//if current char is in the vowels string
            while (start < end && vowels.indexOf(chars[end]) == -1) {
                end--;
            }

			//swap chars
            char temp = chars[start];
            chars[start] = chars[end];
            chars[end] = temp;

			//move to the next char
            start++;
            end--;
        }

        return new String(chars);
    }
}
```

This solution uses two pointers to iterate through the list, and swaps two vowel chars when they are found

Vowels are detected by using a string of vowels, and then calling `indexOf` to see if the current character is present in the vowel array