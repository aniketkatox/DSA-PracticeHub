# Python Code

```python 

class Solution:
    def shortestCommonSupersequence(self, str1: str, str2: str) -> str:
        """
        Finds the shortest common supersequence of two strings.

        Args:
            str1 (str): First input string.
            str2 (str): Second input string.

        Returns:
            str: Shortest common supersequence of str1 and str2.

        """
        memo = [[None] * len(str2) for _ in range(len(str1))]
        result = self.memoizedSolution(str1, str2, 0, 0, memo)

        if len(result) == 0:
            return str1 + str2

        merged = []
        i, j = 0, 0

        for char in result:
            while str1[i] != char:
                merged.append(str1[i])
                i += 1
            while str2[j] != char:
                merged.append(str2[j])
                j += 1
            merged.append(char)
            i += 1
            j += 1

        merged.extend(str1[i:])
        merged.extend(str2[j:])
        return ''.join(merged)

    def memoizedSolution(self, str1: str, str2: str, i: int, j: int, memo: List[List[str]]) -> str:
        """
        Helper function that recursively computes the shortest common supersequence.

        Args:
            str1 (str): First input string.
            str2 (str): Second input string.
            i (int): Current index in str1.
            j (int): Current index in str2.
            memo (List[List[str]]): Memoization table to store computed results.

        Returns:
            str: Shortest common supersequence of str1[i:] and str2[j:].

        """
        if i >= len(str1) or j >= len(str2):
            return ''

        if memo[i][j] is not None:
            return memo[i][j]

        if str1[i] == str2[j]:
            memo[i][j] = str1[i] + self.memoizedSolution(str1, str2, i + 1, j + 1, memo)
        else:
            left = self.memoizedSolution(str1, str2, i + 1, j, memo)
            right = self.memoizedSolution(str1, str2, i, j + 1, memo)
            memo[i][j] = left if len(left) >= len(right) else right

        return memo[i][j]


```


## Time Complexity
- The function memoizedSolution is called recursively to find the shortest common supersequence. Let's denote the lengths of str1 and str2 as m and n respectively.

The recursive calls explore all possible combinations of characters from str1 and str2. In the worst case, each character of str1 can match with every character of str2, resulting in a branching factor of O(n) at each recursive call.

Considering the memoization technique, once a subproblem is computed, it is stored in the memo array. Subsequent recursive calls for the same subproblem can directly retrieve the result from the memo array, resulting in constant time lookup.

Therefore, the overall time complexity of the shortestCommonSupersequence function is O(m * n), where m is the length of str1 and n is the length of str2

## Space Complexity

- The space complexity is determined by the memoization table and the size of the output string.

The memoization table memo is a 2D array of size m x n, where m and n are the lengths of str1 and str2 respectively. Hence, the space required by the memo table is O(m * n).

The output string merged stores the shortest common supersequence, which can have a maximum length of m + n. Therefore, the space required to store the output string is O(m + n).

**Note**

-  space complexity can be further optimized by using a 1D memoization array instead of a 2D array, reducing it to O(n) since only one row of the memoization table is used at a time. However, the time complexity remains the same.
