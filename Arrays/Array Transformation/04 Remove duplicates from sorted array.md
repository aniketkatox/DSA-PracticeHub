# Python Code

```python

class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        """
        Remove duplicates from the sorted input array in-place and return the new length.

        Args:
            nums: The input array of integers.

        Returns:
            int: The new length of the array after removing duplicates.

        """

        shift = 0  # Variable to keep track of the shifting or displacement of duplicate elements

        for i in range(1, len(nums)):
            if nums[i] == nums[i - 1]:
                shift += 1  # Increment the shift count if the current element is a duplicate
            else:
                nums[i - shift] = nums[i]  # Shift the non-duplicate element to its correct position

        return len(nums) - shift


```
