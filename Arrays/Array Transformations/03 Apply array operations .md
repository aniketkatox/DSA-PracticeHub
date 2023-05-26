# Python Code

```python

class Solution:
    def applyOperations(self, nums: List[int]) -> List[int]:
        """
        Apply operations to modify the input array.

        Args:
            nums: The input array of integers.

        Returns:
            List[int]: The modified array.

        """

        shift = 0  # Variable to keep track of the shifting or displacement of non-zero elements
        i = 0  # Iterator variable
        
        while i < len(nums) - 1:
            if nums[i] == nums[i + 1]:
                nums[i] = nums[i] * 2
                nums[i + 1] = 0  # Set the next element to 0 after doubling the current element
            
            if nums[i] == 0:
                shift += 1  # Increment the shift count if the current element is zero
            else:
                # Swap the current non-zero element with the element i-shift positions before it
                nums[i - shift], nums[i] = nums[i], nums[i - shift]

            i += 1

        # Swap the last element with the shifted position to account for the final shift
        nums[i], nums[i - shift] = nums[i - shift], nums[i]

        return nums


```
