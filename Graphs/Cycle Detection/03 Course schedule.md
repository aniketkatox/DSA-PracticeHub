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

**Time Complexity**
- The time complexity of the code is O(V + E), where V is the number of courses (vertices) and E is the number of prerequisites (edges). This is because the code performs a Depth-First Search (DFS) traversal starting from each course, visiting each course and its prerequisites once.

**Space Complexity**
- The space complexity of the code is O(V), where V is the number of courses. This is primarily due to the space used by the color array, which stores the color (visited status) of each course. Additionally, the recursive DFS function call stack requires space proportional to the maximum depth of the recursion, which is bounded by the number of courses. Overall, the space complexity is linear with respect to the number of courses.
