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
