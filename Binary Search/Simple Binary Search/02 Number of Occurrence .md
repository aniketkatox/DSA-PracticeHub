# Python Code

```python 

class Solution:
    def count(self, arr, n, x):
        """
        Counts the number of occurrences of x in a sorted array arr.

        Args:
            arr (List[int]): The sorted array of integers.
            n (int): The size of the array.
            x (int): The number to count occurrences of.

        Returns:
            int: The number of occurrences of x in arr.

        Complexity Analysis:
            Time Complexity: O(log n), where n is the size of the array arr.
            Space Complexity: O(1), since the algorithm uses only a constant amount of extra space.
        """

        # Find the first occurrence of x using binary search
        first_index = self.findFirst(arr, n, x)

        # If x is not found, return 0
        if first_index == -1:
            return 0

        # Find the last occurrence of x using binary search
        last_index = self.findLast(arr, n, x)

        # Return the count of occurrences
        return last_index - first_index + 1

    def findFirst(self, arr, n, x):
        # Binary search to find the first occurrence of x
        low = 0
        high = n - 1
        result = -1

        while low <= high:
            mid = low + (high - low) // 2

            if arr[mid] == x:
                result = mid
                high = mid - 1
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1

        return result

    def findLast(self, arr, n, x):
        # Binary search to find the last occurrence of x
        low = 0
        high = n - 1
        result = -1

        while low <= high:
            mid = low + (high - low) // 2

            if arr[mid] == x:
                result = mid
                low = mid + 1
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1

        return result

```
