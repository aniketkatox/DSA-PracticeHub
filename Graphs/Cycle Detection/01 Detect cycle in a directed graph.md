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
