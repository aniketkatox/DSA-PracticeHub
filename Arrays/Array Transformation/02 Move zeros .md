# Python Code

```python

class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Move all zeros to the end of the array in-place.

        Args:
            nums: The input array of integers.

        Returns:
            None. Modifies the input array in-place.

        """

        shift = 0  # Variable to keep track of the shifting or displacement of zeros
        
        for i in range(len(nums)):
            if nums[i] == 0:
                shift += 1  # Increment the shift count if the current element is zero
            else:
                nums[i - shift], nums[i] = nums[i], nums[i - shift]  # Swap the current element with the non-zero element before it
        
        # The array is modified in-place with zeros moved to the end


```
