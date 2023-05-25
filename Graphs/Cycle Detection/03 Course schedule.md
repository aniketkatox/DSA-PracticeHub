# Python Code

```python

class Solution:
    def canFinish(self, n: int, pre: List[List[int]]):
        # Problem is essentially finding a cycle in a directed graph
        # We can use either DFS or BFS (Kahn's algorithm) to solve it
        
        # Create the graph
        self.graph = {i: [] for i in range(n)}
        for edge in pre:
            a, b = edge[0], edge[1]
            self.graph[b].append(a)  # Append outgoing edges of vertex b
        
        self.color = ['white' for i in range(n)]  # Initialize color array
        
        for i in range(n):
            if self.color[i] == 'white':
                if self.dfs(i) == False:  # If encounter False in any function call, return False
                    return False
        return True
    
    def dfs(self, source):
        self.color[source] = 'grey'
        
        for neighbor in self.graph[source]:
            if self.color[neighbor] == 'grey':  # If encounter unfinished edge, cycle is found
                return False  # Returning False means can't finish all the courses
            
            elif self.color[neighbor] == 'white':
                if self.dfs(neighbor) == False:
                    return False
        
        self.color[source] = 'black'
        return True



```
