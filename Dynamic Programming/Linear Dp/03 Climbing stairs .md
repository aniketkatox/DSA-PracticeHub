# Python Code


```python 

class Solution:
    def climbStairs(self, n: int) -> int:
        """
        Calculates the number of distinct ways to climb to the top of a staircase with n steps.
        
        Args:
            n (int): The total number of steps in the staircase.
        
        Returns:
            int: The number of distinct ways to climb the staircase.
        """
        self.dp = [-1 for i in range(n+1)]  # Memoization table
        
        return self.helper(n)
    
    def helper(self, n):
        """
        Helper function to calculate the number of distinct ways to climb the staircase using dynamic programming.
        
        Args:
            n (int): The total number of steps in the staircase.
        
        Returns:
            int: The number of distinct ways to climb the staircase.
        """
        if n == 1 or n == 2:
            return n
        
        if self.dp[n] != -1:
            return self.dp[n]
        
        # Calculate and memoize the number of distinct ways to climb the staircase
        self.dp[n] = self.helper(n-1) + self.helper(n-2)
        return self.dp[n]


```

**Time Complexity**
- The time complexity of this solution is O(n) because we calculate the number of distinct ways to climb the staircase up to n steps only once and then store the intermediate results in the memoization table.

**Space Complexity**
- The space complexity is O(n) as well since we use the memoization table of size n+1 to store the computed results.
