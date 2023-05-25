# Python Code

```python

class Solution:
    def isCycle(self, V, adj):
        # Initialize an array to keep track of colors of nodes
        self.color = ['white'] * V
        
        # Traverse each node and check for cycles
        for i in range(V):
            if self.color[i] == 'white':
                if self.dfs(i, adj, -1):
                    return True
        return False
    
    def dfs(self, u, adj, prev):
        # Mark the current node as grey (visited)
        self.color[u] = 'grey'
        
        # Traverse all adjacent nodes of the current node
        for v in adj[u]:
            # If an adjacent node is already grey and not the previous node,
            # then a cycle exists
            if self.color[v] == 'grey' and prev != v:
                return True
            # If an adjacent node is white (unvisited), recursively call dfs on it
            elif self.color[v] == 'white':
                # Pass the current node as the previous node to the next dfs call
                if self.dfs(v, adj, u):
                    return True
        
        # Mark the current node as black (fully explored)
        self.color[u] = 'black'
        return False


```

**Time Complexity**
- The time complexity of the code is O(V + E), where V is the number of vertices and E is the number of edges in the graph represented by the adjacency list adj. This is because the code performs a Depth-First Search (DFS) traversal starting from each vertex, visiting each vertex and edge once.

**Space Complexity**
- The space complexity of the code is O(V), where V is the number of vertices. This is primarily due to the space used by the color array, which stores the color (visited status) of each vertex. Additionally, the recursive DFS function call stack requires space proportional to the maximum depth of the recursion, which is bounded by the number of vertices. Overall, the space complexity is linear with respect to the number of vertices in the graph.

