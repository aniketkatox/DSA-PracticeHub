# Python Code

```python

class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        """
        Returns the number of unique paths from the top-left corner to the bottom-right corner of a grid.

        Args:
            m (int): The number of rows in the grid.
            n (int): The number of columns in the grid.

        Returns:
            int: The number of unique paths.

        Examples:
            uniquePaths(3, 2) returns 3, as there are 3 unique paths from the top-left to the bottom-right corner.
        """
        # Base case: if the grid has only one cell, return 1
        if m == 1 and n == 1:
            return 1

        # Initialize a memoization table to store calculated results
        self.dp = [[-1 for j in range(n)] for i in range(m)]

        # Invoke the helper function to calculate the number of unique paths
        self.helper(m - 1, n - 1, m, n)

        # Return the result stored in the bottom-right cell of the grid
        return self.dp[-1][-1]

    def helper(self, i, j, m, n):
        """
        Recursive helper function to calculate the number of unique paths.

        Args:
            i (int): The current row index.
            j (int): The current column index.
            m (int): The total number of rows in the grid.
            n (int): The total number of columns in the grid.

        Returns:
            int: The number of unique paths from the current cell to the bottom-right corner.
        """
        # Base case: if the current cell is out of bounds, return 0
        if i < 0 or j < 0:
            return 0

        # Base case: if the current cell is the top-left corner, return 1
        if i == 0 and j == 0:
            return 1

        # If the result is already calculated, return the stored result
        if self.dp[i][j] != -1:
            return self.dp[i][j]

        # Calculate the number of unique paths by summing the paths from the left and upper cells
        left = self.helper(i - 1, j, m, n)
        upper = self.helper(i, j - 1, m, n)

        # Store the calculated result in the memoization table
        self.dp[i][j] = left + upper

        # Return the result
        return self.dp[i][j]

```

**Time Complexity**
- The time complexity of this solution is O(m * n) because each cell in the grid is visited once and its result is stored in the memoization table. The number of unique paths for each cell is calculated by considering the left and upper cells, resulting in a linear time complexity proportional to the size of the grid.

**Space Complexity**
- The space complexity is also O(m * n) because the memoization table is created to store the calculated results for each cell in the grid. The space required is proportional to the size of the grid.
-
