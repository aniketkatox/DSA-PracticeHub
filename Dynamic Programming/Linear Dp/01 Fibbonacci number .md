# Python Code

```python

class Solution:
    def fib(self, n):
        """
        Calculates the nth Fibonacci number using dynamic programming.

        Args:
            n (int): The index of the Fibonacci number to calculate.

        Returns:
            int: The nth Fibonacci number.

        """
        self.dp = [-1 for i in range(n + 1)]

        return self.helper(n)

    def helper(self, n):
        """
        Helper function to calculate the nth Fibonacci number using memoization.

        Args:
            n (int): The index of the Fibonacci number to calculate.

        Returns:
            int: The nth Fibonacci number.

        """
        # Base cases
        if n == 0 or n == 1:
            return n

        # Check if the result is already computed
        if self.dp[n] != -1:
            return self.dp[n]

        # Compute the result using recursion
        self.dp[n] = self.helper(n - 1) + self.helper(n - 2)
        return self.dp[n]


```

**Time Complexity Analysis:**
The time complexity of this solution is O(n) because we compute the Fibonacci number for each index from 2 to n exactly once. Each computation takes constant time since we use memoization to avoid redundant calculations.

**Space Complexity**
The space complexity of this solution is O(n) because we use an additional array self.dp of size n+1 to store the computed Fibonacci numbers.
