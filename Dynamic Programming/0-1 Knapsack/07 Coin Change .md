# Python Code 

```python 

class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        """
        Calculates the minimum number of coins needed to make the given amount.

        Args:
            coins (List[int]): List of coin denominations.
            amount (int): Target amount.

        Returns:
            int: Minimum number of coins needed to make the target amount. Returns -1 if it is not possible.

        """
        dp = [[False for _ in range(amount + 1)] for _ in range(len(coins) + 1)]
        
        output = self.calculateMinCoins(coins, len(coins), amount, dp)
       
        if output == float("inf"):
            return -1
        return output
        
    def calculateMinCoins(self, coins, n, amount, dp):
        """
        Helper function to calculate the minimum number of coins needed.

        Args:
            coins (List[int]): List of coin denominations.
            n (int): Current index of the coin denomination.
            amount (int): Current amount to be made.
            dp (List[List[bool]]): DP table to store computed values.

        Returns:
            int: Minimum number of coins needed to make the target amount. Returns float('inf') if it is not possible.

        """
        if amount == 0:
            return 0
        
        if n == 0:
            return float("inf")
        
        if dp[n][amount] != False: 
            return dp[n][amount]
        
        if coins[n - 1] <= amount:
            include = 1 + self.calculateMinCoins(coins, n, amount - coins[n - 1], dp)
            exclude = self.calculateMinCoins(coins, n - 1, amount, dp)
            
            dp[n][amount] = min(include, exclude)
            
            return dp[n][amount]
        else:
            dp[n][amount] = self.calculateMinCoins(coins, n - 1, amount, dp)
            
            return dp[n][amount]

```

**Time Complexity**
- The time complexity of this solution is O(n * amount), where n is the number of coin denominations and amount is the target amount. This is because we have n * amount subproblems to solve, and for each subproblem, we have two choices: include the current coin or exclude it.

**Space Complexity**
- The space complexity is also O(n * amount). We use a 2D dp table of size (n+1) x (amount+1) to store the computed results. Each cell in the table represents the minimum number of coins needed to make a particular amount using a subset of the coin denominations. We have n x amount subproblems in total, so the space required is proportional to the number of subproblems.
