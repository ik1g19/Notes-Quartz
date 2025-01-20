Begins with a node, then first traverses all its adjacent

Once all adjacent are visited, then their adjacent are traversed

Closest vertices are visited before others

# Algorithm


- Initialization: Enqueue the given source vertex into a queue and mark it as visited
- Exploration: While the queue is not empty:
	- Dequeue a node from the queue and visit it (e.g., print its value)
	- For each unvisited neighbour of the dequeued node:
		- Enqueue the neighbour into the queue
		- Mark the neighbour as visited
- Termination: Repeat step 2 until the queue is empty

![[Images/bfs.gif]]

# Implementation

```java
// BFS from given source s
static void bfs(List<List<Integer>> adj, int s) {
  
	// Create a queue for BFS
	Queue<Integer> q = new LinkedList<>();
	
	// Initially mark all the vertices as not visited
	// When we push a vertex into the q, we mark it as 
	// visited
	boolean[] visited = new boolean[adj.size()];
	
	// Mark the source node as visited and enqueue it
	visited[s] = true;
	q.add(s);
	
	// Iterate over the queue
	while (!q.isEmpty()) {
	  
		// Dequeue a vertex and print it
		int curr = q.poll();
		System.out.print(curr + " ");
		
		// Get all adjacent vertices of the dequeued vertex
		// If an adjacent has not been visited, mark it 
		// visited and enqueue it
		for (int x : adj.get(curr)) {
			if (!visited[x]) {
				visited[x] = true;
				q.add(x);
			}
		}
	}
}
```

