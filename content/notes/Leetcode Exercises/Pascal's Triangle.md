#leetcode

# Question

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![|200](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

**Input:** numRows = 5
**Output:** \[\[1\],\[1,1\],\[1,2,1\],\[1,3,3,1\],\[1,4,6,4,1\]\]

**Example 2:**

**Input:** numRows = 1
**Output:** \[\[1\]\]

# Solution

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(List.of(1));

        for (int i = 1; i < numRows; i++) {
            List<Integer> newRow = new ArrayList<>();
            List<Integer> lastRow = ans.get(i-1);
            List<Integer> dummyRow = new ArrayList<>(lastRow);

            dummyRow.add(0,0);
            dummyRow.add(dummyRow.size(), 0);

            for (int j = 0; j < dummyRow.size()-1; j++) {
                newRow.add(dummyRow.get(j) + dummyRow.get(j+1));
            }

            ans.add(newRow);
        }

        return ans;
    }
}
```

This is a dynamic programming approach as it stores each row as a result and uses it to compute a future row

Add a 0 to the start and end of the current row, you can then compute each digit of the next row by adding each pair in the current row