# Question

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

- Only numbers `1` through `9` are used.
- Each number is used **at most once**.

Return _a list of all possible valid combinations_. The list must not contain the same combination twice, and the combinations may be returned in any order.

**Example 1:**

**Input:** k = 3, n = 7
**Output:** \[\[1,2,4]]
**Explanation:**
1 + 2 + 4 = 7
There are no other valid combinations.

**Example 2:**

**Input:** k = 3, n = 9
**Output:** \[\[1,2,6],\[1,3,5],\[2,3,4]]
**Explanation:**
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.

**Example 3:**

**Input:** k = 4, n = 1
**Output:** \[]
**Explanation:** There are no valid combinations.
Using 4 different numbers in the range \[1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.

# Solution

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans = new ArrayList();
        List<Integer> comb = new ArrayList();
        recurse(ans, comb, 1, k, n);

        return ans;
    }

    private List<List<Integer>> combination(List<List<Integer>> ans, List<Integer> comb, int start, int k, int n) {
        if (comb.size() == k && n == 0) {
            List<Integer> copy = new ArrayList<>(comb);
            ans.add(copy);
            return new ArrayList<>();
        }

        for (int i = start; i <= 9; i++) {
            comb.add(i);
            recurse(ans, comb, i+1, k, n-i);
            comb.remove(comb.size()-1);
        }

        return new ArrayList<>();
    }
}
```

**Parameters:**

- `ans`: The main list storing all valid combinations.
- `comb`: A temporary list storing the current combination being built.
- `k`: The number of elements we want in the combination (still the same as before).
- `start`: The number at which to start adding elements to the combination (used to prevent duplicates and ensure numbers are added in increasing order).
- `n`: The remaining sum that needs to be achieved with the current combination

## Working of combination method

### Base Case

```java
if (comb.size() == k && n == 0) {
    List<Integer> li = new ArrayList<Integer>(comb);
    ans.add(li);
    return;
}
```

If the combination (comb) has exactly k numbers and the sum of numbers in comb equals n (i.e., n == 0), then this is a valid combination

We create a copy of comb and add it to ans. We then return, stopping the current recursion

### Recursive Loop

```java
for (int i = start; i <= 9; i++) {
    comb.add(i);
    combination(ans, comb, k, i+1, n-i);
    comb.remove(comb.size() - 1);
}
```

The loop runs from start to 9 (because the numbers can only be from 1 to 9)

For each number `i` in this range:
- We add `i` to the current combination comb.
- We make a recursive call to combination, reducing the target sum `n` by `i` (i.e., `n - i`) and increasing the start value to `i + 1` to prevent reusing the same numbers.
- After returning from the recursive call, we remove the last added number (backtracking) to explore other combinations.