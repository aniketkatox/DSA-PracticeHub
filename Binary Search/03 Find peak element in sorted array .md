# Python Code

```python

from typing import List

class Solution:
    def findPeakElement(self, A: List[int]) -> int:
        """
        Finds a peak element in the given array A.

        Args:
            A (List[int]): The input array.

        Returns:
            int: The index of a peak element.

        Complexity Analysis:
            Time Complexity: O(log n), where n is the length of the input array A.
            Space Complexity: O(1), since the algorithm uses only a constant amount of extra space.
        """

        # Check if the array has only one element or the first element is a peak
        if len(A) == 1 or A[0] > A[1]:
            return 0

        # Check if the last element is a peak
        if A[-1] > A[-2]:
            return len(A) - 1

        # Perform binary search to find a peak element
        low = 1
        high = len(A) - 2

        while low <= high:
            mid = low + (high - low) // 2

            # Check if the middle element is a peak
            if A[mid - 1] <= A[mid] >= A[mid + 1]:
                return mid
            # If the middle element is not a peak, update the search range
            elif A[mid] < A[mid + 1]:
                low = mid + 1
            else:
                high = mid - 1

        # If a peak element is not found, return -1
        return -1


```
