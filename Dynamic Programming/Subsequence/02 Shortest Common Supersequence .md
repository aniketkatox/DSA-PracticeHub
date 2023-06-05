# Python Code

```python 

class Solution:
    def shortestCommonSupersequence(self, X: str, Y: str, m: int, n: int) -> int:
        """
        Find the length of the shortest common supersequence of strings X and Y.

        Args:
            X (str): First string.
            Y (str): Second string.
            m (int): Length of X.
            n (int): Length of Y.

        Returns:
            int: Length of the shortest common supersequence.

        """
        # Create a 2D dp table to store computed values
        dp = [[-1] * (n + 1) for _ in range(m + 1)]

        # Calculate the length of the shortest common supersequence
        return m + n - self.lcs(X, Y, m, n, dp)

    def lcs(self, X, Y, m, n, dp):
        """
        Helper function to find the length of the longest common subsequence between X and Y.

        Args:
            X (str): First string.
            Y (str): Second string.
            m (int): Length of X.
            n (int): Length of Y.
            dp (List[List[int]]): DP table to store computed values.

        Returns:
            int: Length of the longest common subsequence.

        """
        # Base cases
        if m == 0 or n == 0:
            return 0

        # Check if the value is already computed
        if dp[m][n] != -1:
            return dp[m][n]

        # If the characters at the current indices match
        if X[m - 1] == Y[n - 1]:
            dp[m][n] = 1 + self.lcs(X, Y, m - 1, n - 1, dp)
            return dp[m][n]

        else:
            # Find the maximum length by excluding one character from X or Y
            dp[m][n] = max(self.lcs(X, Y, m - 1, n, dp), self.lcs(X, Y, m, n - 1, dp))
            return dp[m][n]


```

## Time Complexity Analysis:
The time complexity of the shortestCommonSupersequence method is O(m * n), where m and n are the lengths of strings X and Y, respectively. This is because the function calls the lcs method, which has a time complexity of O(m * n). However, due to memoization, the actual time complexity is reduced since repeated subproblems are avoided.

## Space Complexity Analysis:
The space complexity is O(m * n) as well. It is determined by the size of the dp table, which has dimensions (m + 1) x (n + 1). This space is used to store the computed values for each subproblem, allowing for efficient memoization.




