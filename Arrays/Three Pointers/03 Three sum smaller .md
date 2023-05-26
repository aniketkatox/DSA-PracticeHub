# Python Code

```python

class Solution:
    def countTriplets(self, arr, n, target_sum):
        """
        Count the number of triplets in the array whose sum is less than the target sum.

        Args:
            arr: The input array of integers.
            n: The length of the array.
            target_sum: The target sum.

        Returns:
            The count of triplets whose sum is less than the target sum.

        """

        # Sort the input array in ascending order
        arr.sort()

        # Initialize the result count
        count = 0

        # Iterate through each element as the first element of the triplet
        for i in range(0, n-2):
            
            # Initialize the other two elements as the corner elements of the subarray arr[j+1..k]
            j = i + 1
            k = n - 1

            # Use the "Meet in the Middle" concept
            while j < k:

                # If the sum of the current triplet is greater or equal to the target sum,
                # move the right corner to look for smaller values
                if arr[i] + arr[j] + arr[k] >= target_sum:
                    k -= 1

                # Else, move the left corner
                else:
                    # This is important. For the current i and j, there can be a total of (k - j) third elements.
                    count += (k - j)
                    j += 1

        return count


```

**Time Complexity**
- The time complexity of the countTriplets method is O(n^2), where n is the length of the arr array. The outer loop runs for (n - 2) iterations, and the inner while loop runs in a two-pointer fashion, taking O(n) iterations in the worst case. Therefore, the overall time complexity is O(n^2).

**Space Complexity**
- The space complexity is O(1) since the algorithm doesn't use any extra space that grows with the input size. It only uses a constant amount of extra space to store some variables during the process.
-
