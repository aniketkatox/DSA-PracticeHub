# Python Code

```python 

class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        """
        Returns the length of the longest palindromic subsequence in the given string.

        Args:
            s (str): Input string.

        Returns:
            int: Length of the longest palindromic subsequence.

        """
        n = len(s)
        memo = [[-1] * (n + 1) for _ in range(n + 1)]
        return self.lcs(s, s[::-1], n, n, memo)
    
    def lcs(self, s1: str, s2: str, m: int, n: int, memo: List[List[int]]) -> int:
        """
        Computes the length of the longest common subsequence between two strings.

        Args:
            s1 (str): First input string.
            s2 (str): Second input string.
            m (int): Length of s1.
            n (int): Length of s2.
            memo (List[List[int]]): Memoization table to store computed results.

        Returns:
            int: Length of the longest common subsequence.

        """
        # Base case: if either of the strings is empty, LCS is 0
        if m == 0 or n == 0:
            return 0

        # If the subproblem has already been solved, return the stored value
        if memo[m][n] != -1:
            return memo[m][n]

        # If the last characters of both strings match
        if s1[m - 1] == s2[n - 1]:
            # Compute LCS for the remaining substrings
            memo[m][n] = 1 + self.lcs(s1, s2, m - 1, n - 1, memo)
            return memo[m][n]
        else:
            # Reduce the problem to subproblems by excluding one character from each string
            memo[m][n] = max(self.lcs(s1, s2, m - 1, n, memo), self.lcs(s1, s2, m, n - 1, memo))
            return memo[m][n]



```

## Time Complexity
- The time complexity of this algorithm is O(n^2), where n is the length of the input string. This is because we iterate over all possible pairs of characters in the string to fill the memoization table.

## Space Complexity
- The space complexity is also O(n^2) because we use a memoization table of size (n + 1) x (n + 1) to store the computed results. Additionally, the recursive function calls consume stack space proportional to the length of the input string
