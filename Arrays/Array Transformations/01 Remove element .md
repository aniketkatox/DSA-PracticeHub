# Python Code

```python

class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        """
        Remove all instances of the given value from the array in-place and return the new length.

        Args:
            nums: The input array of integers.
            val: The value to be removed.

        Returns:
            The new length of the array after removing the given value.

        """

        shift = 0  # Variable to keep track of the shifting or displacement of elements
        
        for i in range(len(nums)):
            if nums[i] == val:
                shift += 1  # Increment the shift count if the current element is equal to the value to be removed
            else:
                nums[i - shift] = nums[i]  # Shift the current element to its correct position
                
        return len(nums) - shift  # Return the new length of the array after removing the value


```
