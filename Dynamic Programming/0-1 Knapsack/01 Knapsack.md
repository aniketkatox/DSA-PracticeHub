# Python Code

```python 

class Solution:
    def funcn(self, capacity, wt_array, val_array, n):
        """
        Helper function for computing the maximum value that can be achieved in the knapsack.

        Args:
            capacity (int): Remaining capacity of the knapsack.
            wt_array (List[int]): Array of item weights.
            val_array (List[int]): Array of item values.
            n (int): Size of the arrays.

        Returns:
            int: Maximum value achievable with the given capacity and items.

        """

        if n <= 0:
            return 0

        if self.dp[n][capacity] != -1:
            return self.dp[n][capacity]

        if wt_array[n - 1] <= capacity:
            value_considered = val_array[n - 1] + self.funcn(capacity - wt_array[n - 1], wt_array, val_array, n - 1)
            not_considered = 0 + self.funcn(capacity, wt_array, val_array, n - 1)
            self.dp[n][capacity] = max(value_considered, not_considered)
            return self.dp[n][capacity]

        else:
            return self.funcn(capacity, wt_array, val_array, n - 1)

    def knapSack(self, W, wt, val, n):
        """
        Calculates the maximum value that can be achieved in the knapsack.

        Args:
            W (int): Maximum capacity of the knapsack.
            wt (List[int]): Array of item weights.
            val (List[int]): Array of item values.
            n (int): Number of items.

        Returns:
            int: Maximum value achievable in the knapsack.

        """

        self.dp = [[-1 for i in range(0, W + 1)] for j in range(0, n + 1)]
        return self.funcn(W, wt, val, n)

```
**Time Complexity**
- The time complexity of the solution is O(n * W), where n is the number of items and W is the maximum capacity of the knapsack. This is because for each item, we consider two choices (including or excluding the item) and iterate over different capacities. The funcn function is recursively called for n items, each with W different capacities.

**Space Complexity**
- The space complexity of the solution is O(n * W) as well. The dp table has dimensions (n+1) x (W+1), which accounts for the extra row and column for the base cases. This table is used to store the computed values for subproblems, resulting in the space complexity proportional to the number of items and the maximum capacity of the knapsack.
-
