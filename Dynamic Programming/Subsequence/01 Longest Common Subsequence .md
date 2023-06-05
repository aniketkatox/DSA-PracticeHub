# Python Code

```python

class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [[-1] * (n + 1) for _ in range(m + 1)]
        return self.lcs(text1, text2, m, n, dp)
    
    def lcs(self, text1, text2, m, n, dp):
        # Base case: if either of the strings is empty, LCS is 0
        if m == 0 or n == 0:
            return 0
        
        # If the subproblem has already been solved, return the stored value
        if dp[m][n] != -1:
            return dp[m][n]
        
        # If the last characters of both strings match, reduce the problem to the subproblem
        # without the last characters and add 1 to the LCS length
        if text1[m - 1] == text2[n - 1]:
            dp[m][n] = 1 + self.lcs(text1, text2, m - 1, n - 1, dp)
            return dp[m][n]
        
        # If the last characters of both strings do not match, reduce the problem to the subproblems
        # by excluding one character from each string and take the maximum LCS length
        else:
            dp[m][n] = max(self.lcs(text1, text2, m - 1, n, dp), self.lcs(text1, text2, m, n - 1, dp))
            return dp[m][n]


```

**Time Complexity**
- The time complexity of this solution is O(m * n), where m and n are the lengths of text1 and text2, respectively. We have m * n subproblems to solve, and each subproblem takes constant time to compute.

**Space Complexity**
- The space complexity is O(m * n) as well since we use a 2D dp table of size (m+1) x (n+1) to store the computed results. Each cell in the table represents the length of the LCS of the corresponding substrings.

