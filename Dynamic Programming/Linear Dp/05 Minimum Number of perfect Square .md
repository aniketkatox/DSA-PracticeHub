# Python code

```python

import math

class Solution:
    def numSquares(self, n: int) -> int:
        """
        Returns the least number of perfect square numbers that sum to n.

        Args:
            n (int): The input integer.

        Returns:
            int: The least number of perfect square numbers that sum to n.
        """
        # Create a memoization dictionary to store calculated results
        memo = {}

        def helper(target):
            # If the target is a perfect square, return 1
            if target == 1 or target == 0:
                return target;
            # If the result is already computed, return the stored result
            if target in memo:
                return memo[target];

            # Initialize the result to the maximum possible value
            result = float('inf')

            # Try all possible perfect square numbers less than or equal to the target
            i = 1;
            while i*i <= target:
                # Recursively calculate the result for the remaining sum
                remaining = target - i * i;
                result    = min(result,1 + helper(remaining))
                i += 1;

            # Store the calculated result in the memoization dictionary
            memo[target] = result
            return result

        return helper(n)


```

**Time COmplexity**
- The time complexity of this solution is O(n * sqrt(n)), where n is the input integer. The loop iterates sqrt(n) times, and for each iteration, a recursive call to helper is made. Since the recursive calls are memoized, the time complexity is significantly reduced.

**Space Complexity**
- The space complexity is O(n) due to the memoization dictionary, which can store results for values up to n.
