# Python code

```python

class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        """
        Finds the first missing positive integer in the given list.
        
        Args:
            nums: List of integers.
        
        Returns:
            The first missing positive integer.
        """
        i = 0
        
        # Perform cyclic sort to place each positive integer in its correct position
        while i < len(nums):
            # Check if the current number is within the valid range and not in its correct position
            if nums[i] > 0 and nums[i] < len(nums) and nums[i] != nums[nums[i] - 1]:
                # Swap the current number with the number at its correct position
                nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]
            else:
                # Move to the next number
                i += 1
        
        # Iterate through the sorted list to find the first missing positive integer
        for i in range(len(nums)):
            if nums[i] != i + 1:
                return i + 1
        
        # If all positive integers are present, return the next positive integer
        return len(nums) + 1


```


**Time Complexity**
- he time complexity of the firstMissingPositive function is O(n), where n is the length of the input list nums. This is because we perform a cyclic sort on the list, which requires iterating over each element at most once.

**Space Complexity**
- The space complexity is O(1) because we are modifying the input list in-place and using only a constant amount of extra space for the loop variables and temporary storage during swaps.
