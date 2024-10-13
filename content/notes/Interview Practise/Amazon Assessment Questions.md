#algorithm #interview-questions

# Amazon Q1

%%[[notes/Interview Practise/Amazon Qs/20240820_154459.pdf#page=2&rect=85,574,533,755&color=red|Amazon Q1 PDF Link]]%%

![[Images/20240820_154459.png]]

## Amazon Q1 Example

%%[[notes/Interview Practise/Amazon Qs/20240820_154459.pdf#page=2&rect=87,418,491,566&color=yellow|Example PDF Link]]%%

![[Images/20240820_154459 3.png]]





# Amazon Q2

%%[[notes/Interview Practise/Amazon Qs/20240820_154459.pdf#page=1&rect=120,570,527,762&color=red|Amazon Q2 PDF Link]]%%

![[Images/20240820_154459 1.png]]

## Amazon Q2 Example

%%[[notes/Interview Practise/Amazon Qs/20240820_154459.pdf#page=1&rect=123,344,501,555&color=yellow|Example PDF Link]]%%

![[Images/20240820_154459 2.png]]

## Solution

```python
import numpy as np
x = np.array([1, 2, 3, 4, 5, 1000, 1001, 1002])
# Sum of the first k elements.
sums = np.insert(np.cumsum(x), 0, 0)
N = len(x)
# Split is the index of the last element in the first half.
split = np.arange(N-1)
# The median positions.
i1 = (split + 1)//2
i2 = split + (N - split)//2
# From start to before i1.
e1 = x[i1]*i1 - sums[i1]
# From after i2 to the split.
e2 = sums[split+1] - sums[i1] - x[i1]*(split - i1 + 1)
# From the split to before i2.
e3 = x[i2]*(i2 - split - 1) - sums[i2] + sums[split+1]
# From after i2 to the end.
e4 = sums[-1] - sums[i2 + 1] - x[i2]*(N - i2 - 1)
error = e1 + e2 + e3 + e4
best = np.argmin(error)
print(f"best x1: {x[i1[best]]}, x2: {x[i2[best]]}, error: {error[best]}")
# best x1: 3, x2: 1001, error: 8
```

Given an array `x`, the goal is to divide it into two contiguous subarrays in a way that minimizes the sum of absolute differences between elements of each subarray and their respective median values. The median of a subarray minimizes the sum of absolute differences within that subarray, so the task reduces to finding the split that minimizes the total error for both subarrays

### Initialization

```python
x = np.array([1, 2, 3, 4, 5, 1000, 1001, 1002])
sums = np.insert(np.cumsum(x), 0, 0)
```

The array `x` is the input array. `sums` is the cumulative sum of elements of `x`, with a zero prepended at the start to simplify index calculations

### Splitting Indices

```python
N = len(x)
split = np.arange(N-1)
```

The array `split` represents the indices where the array can be split. For an array of length `N`, there are `N-1` possible split points


> [!INFO] np.arange
> Returns evenly spaced values within a given interval
> `np.arange(3)` = `array([0, 1, 2])`

### Median Index Calculations

```python
i1 = (split + 1)//2
i2 = split + (N - split)//2
```

#### Understanding `i1`:

- `split + 1`: This is the size of the first subarray for each possible split.
- `(split + 1)//2`: This gives the index of the median element in the first subarray.
    - If the subarray has an odd number of elements, this points to the middle element.
    - If the subarray has an even number of elements, it points to the element just before the middle (assuming zero-based indexing).

```python
i1 = (split + 1) // 2
# split + 1 = [1, 2, 3, 4, 5, 6, 7] 
# i1 = [0, 1, 1, 2, 2, 3, 3]
```

#### Understanding `i2`:

- `split`: This is the index of the last element in the first subarray, so `split + 1` is the starting index of the second subarray.
- `N - split`: This is the size of the second subarray.
- `(N - split)//2`: This gives the position of the median within the second subarray.
- `split + (N - split)//2`: Adding this to `split` moves the median position relative to the entire array `x`

```python
i2 = split + (N - split) // 2
# N - split = [8, 7, 6, 5, 4, 3, 2]
# (N - split) // 2 = [4, 3, 3, 2, 2, 1, 1]
# i2 = [4, 4, 5, 5, 6, 6, 7]
```

### Calculating Errors

```python
e1 = x[i1]*i1 - sums[i1]
e2 = sums[split+1] - sums[i1] - x[i1]*(split - i1 + 1)
e3 = x[i2]*(i2 - split - 1) - sums[i2] + sums[split+1]
e4 = sums[-1] - sums[i2 + 1] - x[i2]*(N - i2 - 1)
error = e1 + e2 + e3 + e4
```

This is where the code calculates the "error" for each possible split. The error is defined as the sum of absolute differences between elements and the median in each subarray

```python
e1 = x[i1]*i1 - sums[i1]
```

`e1`: Error before the median in the first subarray

- `x[i1]*i1`: This is the sum of the median value `x[i1]` multiplied by the number of elements before the median.
- `sums[i1]`: This is the sum of the elements before the median.
- `e1` is the sum of differences between the elements before the median and the median itself.


> [!INFO] Fancy Indexing
> When you index a NumPy array `x` with another array `i`, like `x[i]`, NumPy returns an array where each element is the value of `x` at the corresponding index in `i`. So if `i1` is an array of indices, `x[i1]` returns an array of elements from `x` corresponding to those indices
> `x = np.array([10, 20, 30, 40, 50])`
> `i = np.array([0, 2, 4])`
> `x[i]` will give `array([10, 30, 50])`

`e2`: Error from the median to the split in the first subarray

```python
e2 = sums[split+1] - sums[i1] - x[i1]*(split - i1 + 1)
```

- `sums[split+1] - sums[i1]`: This gives the sum of elements from the median to the split point.
- `x[i1]*(split - i1 + 1)`: This is the sum of the median value multiplied by the number of elements in this range.
- `e2` is the sum of differences between the elements after the median and the median itself, up to the split

`e3`: Error before the median in the second subarray

```python
e3 = x[i2]*(i2 - split - 1) - sums[i2] + sums[split+1]
```

- `x[i2]*(i2 - split - 1)`: This is the sum of the median value `x[i2]` multiplied by the number of elements before the median in the second subarray.
- `sums[i2] - sums[split+1]`: This is the sum of elements from the split point to the median in the second subarray.
- `e3` is the sum of differences between the elements before the median and the median itself in the second subarray

`e4`: Error after the median in the second subarray

```python
e4 = sums[-1] - sums[i2 + 1] - x[i2]*(N - i2 - 1)
```

- `sums[-1] - sums[i2 + 1]`: This is the sum of elements after the median in the second subarray.
- `x[i2]*(N - i2 - 1)`: This is the sum of the median value `x[i2]` multiplied by the number of elements after the median.
- `e4` is the sum of differences between the elements after the median and the median itself in the second subarray

The total error `error = e1 + e2 + e3 + e4` combines the errors from all parts of the two subarrays. The best split point is the one that minimizes this total error. The code then finds this split point using `np.argmin(error)` and returns the corresponding medians and the minimal error

### Java Version

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] x = {1, 2, 3, 4, 5, 1000, 1001, 1002};

        // Calculate the cumulative sum
        int N = x.length;
        int[] sums = new int[N + 1];
        for (int i = 1; i <= N; i++) {
            sums[i] = sums[i - 1] + x[i - 1];
        }

        // Split is the index of the last element in the first half.
        int[] split = new int[N - 1];
        for (int i = 0; i < N - 1; i++) {
            split[i] = i;
        }

        // The median positions.
        int[] i1 = new int[N - 1];
        int[] i2 = new int[N - 1];
        for (int i = 0; i < N - 1; i++) {
            i1[i] = (split[i] + 1) / 2;
            i2[i] = split[i] + (N - split[i]) / 2;
        }

        // Compute the errors
        int[] e1 = new int[N - 1];
        int[] e2 = new int[N - 1];
        int[] e3 = new int[N - 1];
        int[] e4 = new int[N - 1];
        int[] error = new int[N - 1];

        for (int i = 0; i < N - 1; i++) {
            e1[i] = x[i1[i]] * i1[i] - sums[i1[i]];
            e2[i] = sums[split[i] + 1] - sums[i1[i]] - x[i1[i]] * (split[i] - i1[i] + 1);
            e3[i] = x[i2[i]] * (i2[i] - split[i] - 1) - sums[i2[i]] + sums[split[i] + 1];
            e4[i] = sums[N] - sums[i2[i] + 1] - x[i2[i]] * (N - i2[i] - 1);
            error[i] = e1[i] + e2[i] + e3[i] + e4[i];
        }

        // Find the minimum error
        int best = 0;
        for (int i = 1; i < error.length; i++) {
            if (error[i] < error[best]) {
                best = i;
            }
        }

        // Print the result
        System.out.println("best x1: " + x[i1[best]] + ", x2: " + x[i2[best]] + ", error: " + error[best]);
    }
}
```