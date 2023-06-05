# Python Code 


```python 

from typing import List

class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        total_sum = sum(nums)
        
        if total_sum % 2 != 0:
            return False
        else:
            target_sum = total_sum // 2
        
        n = len(nums)
        dp = [[-1 for _ in range(target_sum + 1)] for _ in range(n + 1)]
        
        return self.canPartitionHelper(nums, n, target_sum, dp)
    
    def canPartitionHelper(self, nums: List[int], n: int, target: int, dp: List[List[int]]) -> bool:
        # Base cases
        if target == 0:
            return True
        if n == 0 or target < 0:
            return False
        
        # If the subproblem has already been solved, return the stored value
        if dp[n][target] != -1:
            return bool(dp[n][target])
        
        # If the current element can be included, consider both cases: include or exclude
        if nums[n - 1] <= target:
            included = self.canPartitionHelper(nums, n - 1, target - nums[n - 1], dp)
            not_included = self.canPartitionHelper(nums, n - 1, target, dp)
            dp[n][target] = int(included or not_included)
        else:
            # If the current element cannot be included, exclude it
            dp[n][target] = int(self.canPartitionHelper(nums, n - 1, target, dp))
        
        return bool(dp[n][target])


```

**Time Complexity**
- The time complexity of the top-down implementation of the "Partition Equal Subset Sum" problem is O(n * target), where n is the length of the input array nums and target is the target sum. This is because for each element in the array, we have two choices: include it or exclude it. Therefore, the total number of recursive calls and computed subproblems is proportional to the number of elements multiplied by the target sum.

**Space Complexity**
- The space complexity is O(n * target) as well. This is because we use a 2D dp table of size (n+1) x (target+1) to store the computed results. Each cell in the table represents the result of a subproblem, and we have n x target subproblems in total. Therefore, the space required is proportional to the number of subproblems.
-
