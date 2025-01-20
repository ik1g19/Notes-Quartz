Traverse all adjacent vertices one by one

When we traverse an adjacent vertex, we completely finish the traversal of all vertices reachable through that adjacent vertex

After we finish traversing one adjacent vertex and its reachable vertices, we move to the next adjacent vertex and repeat the process

# Implementation

```java
// Recursive function for DFS traversal
static void DFSRec(List<List<Integer> > adj,
						  boolean[] visited, int s){
	// Mark the current vertex as visited
	visited[s] = true;

	// Print the current vertex
	System.out.print(s + " ");

	// Recursively visit all adjacent vertices that are
	// not visited yet
	for (int i : adj.get(s)) {
		if (!visited[i]) {
			DFSRec(adj, visited, i);
		}
	}
}

// Main DFS function that initializes the visited array
static void DFS(List<List<Integer> > adj, int s) {
	boolean[] visited = new boolean[adj.size()];
	// Call the recursive DFS function
	DFSRec(adj, visited, s);
}
```

