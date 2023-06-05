# Python Code


```python 


from typing import List

class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        """
        Finds the index where the target would be inserted in a sorted array of distinct integers.

        Args:
            nums (List[int]): The sorted array of distinct integers.
            target (int): The target value to search or insert.

        Returns:
            int: The index where the target would be inserted.

        Complexity Analysis:
            Time Complexity: O(log n), where n is the length of the input array nums.
            Space Complexity: O(1), since the algorithm uses only a constant amount of extra space.
        """

        # Initialize the search boundaries
        low = 0
        high = len(nums) - 1

        # Initialize the index where the target would be inserted
        possibleIndex = len(nums)

        # Binary search loop
        while low <= high:
            # Calculate the middle index
            mid = (low + high) >> 1

            # If the middle element is the target, return its index
            if nums[mid] == target:
                return mid
            # If the middle element is greater than the target,
            # update the possible index and search in the left half
            elif nums[mid] > target:
                possibleIndex = mid
                high = mid - 1
            # If the middle element is less than the target,
            # update the low index and search in the right half
            else:
                low = mid + 1

        # If the target is not found, return the possible index where it would be inserted
        return possibleIndex


```
