#sorting 

%%
[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=64|algorithmics rotated cropped, p.64]]
[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=61|Algorithmics Notes, p.61]]
%%

![[Images/algorithmics rotated cropped 6.png|400]]

%%[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=64&rect=66,356,419,545|algorithmics rotated cropped, p.64]]%%

- Splits the list into subgroups, then regroups them
- Once all elements are split into singleton groups, they are each compared and appended to each other

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=61&selection=6,0,12,22&color=yellow|Algorithmics Notes, p.61]]%%

# Algorithm

```
procedure MergeSort(a, start, end)
    if start < end then
        mid ← (start + end) / 2
        MergeSort(a, start, mid)
        MergeSort(a, mid + 1, end)
        Merge(a, start, mid, end)
    else
        return
```

```java
// Merge two subarrays of arr[]: arr[l..m] and arr[m+1..r]
static void merge(int arr[], int l, int m, int r) {
	int n1 = m - l + 1, n2 = r - m;
	int L[] = new int[n1], R[] = new int[n2];

	// Copy data to temp arrays
	System.arraycopy(arr, l, L, 0, n1);
	System.arraycopy(arr, m + 1, R, 0, n2);

	// Merge temp arrays back into arr[]
	int i = 0, j = 0, k = l;
	while (i < n1 && j < n2)
		arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];

	// Copy remaining elements of L[] and R[] (if any)
	while (i < n1) arr[k++] = L[i++];
	while (j < n2) arr[k++] = R[j++];
}

// Recursively sort arr[l..r] using merge()
static void sort(int arr[], int l, int r) {
	if (l < r) {
		int m = l + (r - l) / 2; // Find midpoint
		sort(arr, l, m);        // Sort first half
		sort(arr, m + 1, r);    // Sort second half
		merge(arr, l, m, r);    // Merge sorted halves
	}
}
```

# Example

![[Images/Algorithmics Notes 2.png]]

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=61&rect=70,104,528,293&color=yellow|Algorithmics Notes, p.61]]%%

![[Images/merge-sort.gif|400]]