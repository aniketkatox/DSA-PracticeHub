# Python Code


```python


class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        """
        Remove duplicates from the input array in-place and return the new length.

        Args:
            nums: The input array of integers.

        Returns:
            int: The new length of the array after removing duplicates.

        """

        shift = 0  # Variable to keep track of the shifting or displacement of duplicate elements

        for i in range(len(nums)):
            # Check if the current element is equal to the next two elements
            if i < len(nums) - 2 and nums[i] == nums[i + 1] == nums[i + 2]:
                shift += 1  # Increment the shift count if it is a duplicate
            else:
                nums[i - shift] = nums[i]  # Shift the non-duplicate element to its correct position

        return len(nums) - shift


```
