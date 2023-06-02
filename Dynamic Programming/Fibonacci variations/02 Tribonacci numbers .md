# Python Code


```python

class Solution:
    def tribonacci(self, n: int) -> int:
        """
        Calculates the nth Tribonacci number.
        
        Args:
            n (int): The index of the Tribonacci number to calculate.
        
        Returns:
            int: The nth Tribonacci number.
        """
        self.dp = [-1 for i in range(n+1)]  # Memoization table
        
        return self.helper(n)
    
    def helper(self, n):
        """
        Helper function to calculate the nth Tribonacci number using dynamic programming.
        
        Args:
            n (int): The index of the Tribonacci number to calculate.
        
        Returns:
            int: The nth Tribonacci number.
        """
        if n == 0 or n == 1:
            return n
        elif n == 2:
            return 1
        
        if self.dp[n] != -1:
            return self.dp[n]
        
        # Calculate and memoize the Tribonacci number
        self.dp[n] = self.helper(n-1) + self.helper(n-2) + self.helper(n-3)
        return self.dp[n]


```

**Time Complexity:** 
- The time complexity of this solution is O(n) because we calculate the Tribonacci number up to index n only once and then store the intermediate results in the memoization table.

**Space Complexity:** 
- The space complexity is O(n) as well since we use the memoization table of size n+1 to store the computed Tribonacci numbers.
