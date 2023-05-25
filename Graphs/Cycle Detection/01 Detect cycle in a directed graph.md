# Python Code 

```python

from collections import deque

class Solution:
    def isCyclic(self, V, adj):
        q = deque([])  # Create an empty deque
        
        # Dictionary to store the count of incoming edges for each vertex
        self.dx = {}
        
        self.visited = 0  # Variable to keep track of visited vertices
        
        # Calculate the count of incoming edges for each vertex
        for neighbor_list in adj:
            for neighbor in neighbor_list:
                if neighbor not in self.dx:
                    self.dx[neighbor] = 1
                else:
                    self.dx[neighbor] += 1
        
        # Add vertices with no incoming edges to the queue
        for i in range(V):
            if i not in self.dx:
                q.append(i)
        
        # Perform a BFS traversal starting from vertices with no incoming edges
        while q:
            vertex = q.popleft()  # Dequeue a vertex from the queue
            self.visited += 1  # Increment the visited count
            
            # Reduce the count of incoming edges for neighbors of the dequeued vertex
            for neighbor in adj[vertex]:
                self.dx[neighbor] -= 1
                if self.dx[neighbor] == 0:
                    q.append(neighbor)  # Add neighbors with no remaining incoming edges to the queue
        
        # If all vertices have been visited, it means there is no cycle
        return self.visited != V

```
