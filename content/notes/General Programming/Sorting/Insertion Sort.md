#sorting

%%
[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=58|algorithmics rotated cropped, p.58]]
[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=58|MB Algorithmics Notes, p.58]]
%%

![[Images/algorithmics rotated cropped 5.png|400]]

%%[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=58&rect=74,136,518,402|algorithmics rotated cropped, p.58]]%%

Iteratively inserting each element of an unsorted list into its correct position in a sorted portion of the list

- Start with second element of the array as first element in the array is assumed to be sorted
- Compare second element with the first element and check if the second element is smaller then swap them
- Move to the third element and compare it with the first two elements and put at its correct position
- Repeat until the entire array is sorted

# Algorithm


```
procedure InsertionSort(a)
    for j ← 2 to a.length do
        key ← a[j]
        i ← j - 1
        while i > 0 and a[i] > key do
            a[i + 1] ← a[i]
            i ← i - 1
        end while
        a[i + 1] ← key
    end for
    return a
```

```java
void sort(int arr[]) {
	int n = arr.length;
	for (int j = 1; j < n; ++j) {
		int key = arr[j];
		int i = j - 1;

		
		while (i >= 0 && arr[i] > key) {
			arr[i + 1] = arr[i];
			i = i - 1;
		}
		arr[i + 1] = key;
	}
}
```

Ideal for small arrays
- [[notes/General Programming/Sorting/Stable Sorting|Stable]]
- [[notes/General Programming/Sorting/In-Place Sorting|In-Place]]

# Example

![[Images/Insertion-sorting.png]]

![[Images/Algorithmics Notes 3.png]]

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=58&rect=70,153,527,396|Algorithmics Notes, p.58]]%%