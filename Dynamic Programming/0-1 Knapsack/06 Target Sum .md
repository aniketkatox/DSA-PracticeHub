# Python code

```python 

class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        """
        Calculates the number of ways to reach the target sum using the given numbers.

        Args:
            nums (List[int]): List of integers.
            target (int): Target sum.

        Returns:
            int: Number of ways to reach the target sum.

        """
        if sum(nums) < target:
            return 0

        total_sum = sum(nums)  # Total sum of the numbers in nums
        s1 = total_sum  # Sum of elements in set1 (initially all elements)
        s2 = 0  # Sum of elements in set2 (initially empty)

        dp = [[-1 for _ in range(total_sum + 1)] for _ in range(len(nums) + 1)]
        return self.countWays(nums, len(nums), s1, s2, target, dp)

    def countWays(self, nums, n, s1, s2, target, dp):
        """
        Helper function to count the number of ways to reach the target sum.

        Args:
            nums (List[int]): List of integers.
            n (int): Current index in the list.
            s1 (int): Sum of elements in set1.
            s2 (int): Sum of elements in set2.
            target (int): Target sum.
            dp (List[List[int]]): DP table to store computed values.

        Returns:
            int: Number of ways to reach the target sum.

        """
        if n == 0:
            if s1 - s2 == target:
                return 1
            else:
                return 0

        if dp[n][s1] != -1:
            return dp[n][s1]

        if s1 - s2 >= target:
            taken = self.countWays(nums, n - 1, s1 - nums[n - 1], s2 + nums[n - 1], target, dp)
            not_taken = self.countWays(nums, n - 1, s1, s2, target, dp)
            dp[n][s1] = taken + not_taken
            return dp[n][s1]
        else:
            dp[n][s1] = self.countWays(nums, n - 1, s1, s2, target, dp)
            return dp[n][s1]


```

**Time Complexity**
- The time complexity of this solution is O(n * sum), where n is the length of the input list nums and sum is the sum of all elements in the list. This is because we have n * sum subproblems to solve, and for each subproblem, we have two choices: include the current element in set1 or exclude it.


**Space Complexity**
- The space complexity is O(n * sum) as well. We use a 2D dp table of size (n+1) x (sum+1) to store the computed results. Each cell in the table represents the number of ways to reach the target sum for a particular subproblem, and we have n x sum subproblems in total. Therefore, the space required is proportional to the number of subproblems.

