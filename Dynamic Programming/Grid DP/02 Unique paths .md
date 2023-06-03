# Python Code

```python 

class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        """
        Returns the number of unique paths from the top-left corner to the bottom-right corner of the grid,
        considering the presence of obstacles.

        Args:
            obstacleGrid (List[List[int]]): The grid representing the presence of obstacles.

        Returns:
            int: The number of unique paths.

        Examples:
            uniquePathsWithObstacles([[0,0,0],[0,1,0],[0,0,0]]) returns 2, as there are 2 unique paths.
        """
        # Get the dimensions of the grid
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])

        # Create a memoization table to store calculated results
        self.dp = [[-1 for j in range(n)] for i in range(m)]

        # Invoke the helper function to calculate the number of unique paths
        return self.helper(obstacleGrid, m - 1, n - 1)

    def helper(self, obstacleGrid, i, j):
        """
        Recursive helper function to calculate the number of unique paths.

        Args:
            obstacleGrid (List[List[int]]): The grid representing the presence of obstacles.
            i (int): The current row index.
            j (int): The current column index.

        Returns:
            int: The number of unique paths from the current cell to the bottom-right corner.
        """
        # Base case: if the current cell is out of bounds or an obstacle, return 0
        if i < 0 or j < 0 or obstacleGrid[i][j] == 1:
            return 0

        # If the result is already computed, return the stored result
        if self.dp[i][j] != -1:
            return self.dp[i][j]

        # Base case: if the current cell is the top-left corner, return 1
        if i == 0 and j == 0:
            return 1

        # Calculate the number of unique paths by summing the paths from the left and upper cells
        left = self.helper(obstacleGrid, i, j - 1)
        upper = self.helper(obstacleGrid, i - 1, j)

        # Store the calculated result in the memoization table
        self.dp[i][j] = left + upper

        # Return the result
        return self.dp[i][j]


```

**Time Complexity**
- The time complexity of this solution is O(m * n) because each cell in the grid is visited once and its result is stored in the memoization table.

**Space Complexity**
- The space complexity is also O(m * n) because the memoization table is created to store the calculated results for each cell in the grid. The space required is proportional to the size of the grid.
