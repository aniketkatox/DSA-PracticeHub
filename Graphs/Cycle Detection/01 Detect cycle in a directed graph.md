# Python Code 

```python

class Solution:
    def isCyclic(self, V, adj):
        # Initialize color array for vertices
        self.color = ['white']*V
        # Initialize flag to track cycle presence
        self.flag  = False
        
        # Traverse each vertex
        for i in range(V):
            # If vertex is not visited, perform DFS
            if self.color[i] == 'white':
                self.dfs(i,adj)
        
        # Return the flag indicating cycle presence
        return self.flag
    
    def dfs(self,u,adj):
        # Mark the current vertex as 'grey' to indicate visiting
        self.color[u] = 'grey'
        
        # Traverse each neighbor of the current vertex
        for v in adj[u]:
            # If neighbor is already 'grey', it means there is a cycle
            if self.color[v] == 'grey':
                self.flag = True
            # If neighbor is unvisited, perform DFS on it
            elif self.color[v] == "white":
                self.dfs(v,adj)
                
        # Mark the current vertex as 'black' to indicate completion of visiting
        self.color[u] = 'black'

```
**Time Complexity**
- The time complexity of the code is O(V + E), where V is the number of vertices and E is the number of edges in the graph represented by the adjacency list adj. This is because the code performs a Depth-First Search (DFS) traversal starting from each vertex, and the time complexity of DFS is linear in the number of vertices and edges.

**Space Complexity**
- The space complexity of the code is O(V), where V is the number of vertices. This is primarily due to the space used by the color array, which stores the color (visited status) of each vertex. Additionally, the recursive DFS function call stack requires space proportional to the maximum depth of the recursion, which is bounded by the number of vertices. Overall, the space complexity is linear with respect to the number of vertices in the graph.
