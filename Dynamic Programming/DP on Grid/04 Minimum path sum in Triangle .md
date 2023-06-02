# Python Code

```python

class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        """
        Returns the minimum path sum from top to bottom of the triangle array.

        Args:
            triangle (List[List[int]]): The input triangle array.

        Returns:
            int: The minimum path sum.

        Examples:
            minimumTotal([[2],[3,4],[6,5,7],[4,1,8,3]]) returns 11, as the minimum path sum is 2 + 3 + 5 + 1 = 11.
        """
        # Get the number of rows in the triangle
        n = len(triangle)

        # Create a memoization table to store calculated results
        self.dp = [[-1] * n for _ in range(n)]

        # Invoke the helper function to calculate the minimum path sum
        return self.helper(triangle, 0, 0)

    def helper(self, triangle, row, col):
        """
        Recursive helper function to calculate the minimum path sum.

        Args:
            triangle (List[List[int]]): The input triangle array.
            row (int): The current row index.
            col (int): The current column index.

        Returns:
            int: The minimum path sum from the current cell to the bottom of the triangle.
        """
        # Base case: if the current cell is at the bottom row, return its value
        if row == len(triangle) - 1:
            return triangle[row][col]

        # If the result is already computed, return the stored result
        if self.dp[row][col] != -1:
            return self.dp[row][col]

        # Calculate the minimum path sum by choosing the minimum of the path from the left and the path from the right
        path_left    = self.helper(triangle, row + 1, col)
        path_right   = self.helper(triangle, row + 1, col + 1)
        min_path_sum = min(path_left, path_right) + triangle[row][col]

        # Store the calculated result in the memoization table
        self.dp[row][col] = min_path_sum

        # Return the result
        return min_path_sum


```

**Time Complexity**
- The time complexity of this solution is O(n^2), where n is the number of rows in the triangle. Each cell in the triangle is visited once, and its result is stored in the memoization table.

**Space Complexity**
- he space complexity is also O(n^2) because the memoization table is created to store the calculated results for each cell in the triangle. The space required is proportional to the size of the triangle.
