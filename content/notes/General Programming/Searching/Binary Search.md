Repeatedly divides the search interval in half until the target value is found or the interval is empty 🔗[GfG](https://www.geeksforgeeks.org/binary-search/)

- Data structure must be sorted.
- Access to any element of the data structure should take constant time

# Algorithm

- Divide the search space into two halves by finding the middle index `mid`
- Compare the middle element of the search space with the key
- If the key is found at middle element, the process is terminated
- If the key is not found at middle element, choose which half will be used as the next search space
	- If the key is smaller than the middle element, then the left side is used for next search
	- If the key is larger than the middle element, then the right side is used for next search
- This process is continued until the key is found or the total search space is exhausted

# Implementation

```java
// Java implementation of iterative Binary Search

import java.io.*;

class BinarySearch {
  
    // Returns index of x if it is present in arr[].
    int binarySearch(int arr[], int x)
    {
        int low = 0, high = arr.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;

            // Check if x is present at mid
            if (arr[mid] == x)
                return mid;

            // If x greater, ignore left half
            if (arr[mid] < x)
                low = mid + 1;

            // If x is smaller, ignore right half
            else
                high = mid - 1;
        }

        // If we reach here, then element was
        // not present
        return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        BinarySearch ob = new BinarySearch();
        int arr[] = { 2, 3, 4, 10, 40 };
        int n = arr.length;
        int x = 10;
        int result = ob.binarySearch(arr, x);
        if (result == -1)
            System.out.println(
                "Element is not present in array");
        else
            System.out.println("Element is present at "
                               + "index " + result);
    }
}
```

# Time Complexity

Time Complexity: 
- Best Case: `O(1)`
- Average Case: `O(log N)`
- Worst Case: `O(log N)`