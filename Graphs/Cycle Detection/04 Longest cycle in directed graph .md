# Python Code

```python 


from collections import defaultdict

class Solution:
    def __init__(self):
        self.answer = -1;

    def dfs(self, node, edges, dist, visit):
        # Mark the current node as visited
        visit[node] = True
        neighbor = edges[node]

        if neighbor != -1 and not visit[neighbor]:
            # If the neighbor is not visited, update the distance and perform DFS on the neighbor
            dist[neighbor] = dist[node] + 1
            self.dfs(neighbor, edges, dist, visit)
        elif neighbor != -1 and neighbor in dist:
            # If the neighbor is already visited and present in the distance map, calculate the cycle length
            self.answer = max(self.answer, dist[node] - dist[neighbor] + 1)

    def longestCycle(self, edges: List[int]) -> int:
        n = len(edges)
        visit = [False] * n

        for i in range(n):
            if not visit[i]:
                # Initialize a distance map for each unvisited node and perform DFS
                dist = defaultdict(int)
                dist[i] = 1
                self.dfs(i, edges, dist, visit)

        return self.answer


```

**Time Complexity**
- The time complexity of the code is O(N), where N is the length of the edges array. This is because the code visits each node in the graph exactly once during the DFS traversal
**Space Complexity**
- The space complexity of the code is O(N) as well. This is primarily due to the space used by the dist map, which stores the distance of each node from the starting node during the DFS traversal. In the worst case, all N nodes could be present in the dist map. Additionally, the visit array requires O(N) space to keep track of visited nodes. Overall, the space complexity is linear with respect to the number of nodes in the graph.
