# Python Code

```python 

class Solution:
    def minDifference(self, arr, n):
        """
        Calculates the minimum difference between two subsets of the given array.

        Args:
            arr (List[int]): Array of integers.
            n (int): Size of the array.

        Returns:
            int: Minimum difference between two subsets.

        """
        total_sum = sum(arr)
        dp = [[-1 for _ in range(total_sum + 1)] for _ in range(n + 1)]
        return self.calculateDifference(arr, n, total_sum, 0, dp)

    def calculateDifference(self, arr, n, sum1, sum2, dp):
        """
        Helper function to calculate the minimum difference between two subsets.

        Args:
            arr (List[int]): Array of integers.
            n (int): Current index in the array.
            sum1 (int): Sum of elements in the first subset.
            sum2 (int): Sum of elements in the second subset.
            dp (List[List[int]]): DP table to store computed values.

        Returns:
            int: Minimum difference between two subsets.

        """
        if n == 0:
            return abs(sum1 - sum2)

        if dp[n][sum1] != -1:
            return dp[n][sum1]

        if sum2 <= sum1:
            included = self.calculateDifference(arr, n - 1, sum1 - arr[n - 1], sum2 + arr[n - 1], dp)
            not_included = self.calculateDifference(arr, n - 1, sum1, sum2, dp)
            dp[n][sum1] = min(included, not_included)
            return dp[n][sum1]

        else:
            dp[n][sum1] = abs(sum2 - sum1)
            return dp[n][sum1]

```

**Time Complexity**
- The time complexity of this solution is O(n * sum), where n is the length of the input array arr and sum is the sum of all elements in the array. This is because we have n * sum subproblems to solve, and for each subproblem, we have two choices: include the current element or exclude it.

**Space Compexity**
- The space complexity is O(n * sum) as well. We use a 2D dp table of size (n+1) x (sum+1) to store the computed results. Each cell in the table represents the minimum difference for a particular subproblem, and we have n x sum subproblems in total. Therefore, the space required is proportional to the number of subproblems.
-
