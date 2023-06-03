# Python Code

```python 


class Solution:
    def longestCommonSubstr(self, S1, S2, n, m):
        # Create a memoization array to store computed results
        memo = []
        for i in range(n + 1):
            memo.append([])
            for j in range(m + 1):
                memo[i].append([-1] * (max(n, m) + 1))
        
        # Call the recursive helper function and return the result
        return self.lcs(S1, S2, n, m, 0, memo)
    
    def lcs(self, S1, S2, n, m, count, memo):
        # Base case: if either of the strings is empty, return the count
        if n == 0 or m == 0:
            return count
        
        # If the result for the current subproblem is already memoized, return it
        if memo[n][m][count] != -1:
            return memo[n][m][count]
        count_1 = count;
        # If the last characters of both strings match, recursively compute the LCS for the remaining substrings
        if S1[n - 1] == S2[m - 1]:
            count_1 = self.lcs(S1, S2, n - 1, m - 1, count + 1, memo);
        count_2  = self.lcs(S1, S2, n, m - 1, 0, memo);
        count_3  = self.lcs(S1, S2, n - 1, m, 0, memo);
        memo[n][m][count] =  max(count_1,max(count_2,count_3));
        return memo[n][m][count];

```

## Time Compexity
- The time complexity of the given solution is O(n * m * k), where n is the length of the first string S1, m is the length of the second string S2, and k is the maximum length of common substrings. This is because for each combination of indices (i, j, count), the solution recursively calls itself three times: (i, j - 1, 0), (i - 1, j, 0), and (i - 1, j - 1, count + 1). Since each recursive call reduces the length of at least one string by 1, the maximum depth of the recursion tree is k. Therefore, the overall time complexity is O(n * m * k).

## Space Complexity 
- The space complexity of the given solution is O(n * m * k), as well. This is because the memoization array, memo, has dimensions of (n + 1) x (m + 1) x (max(n, m) + 1), which requires O(n * m * k) space. Each element in the memoization array stores the length of a common substring, so the total space required is proportional to the product of the three dimensions.

