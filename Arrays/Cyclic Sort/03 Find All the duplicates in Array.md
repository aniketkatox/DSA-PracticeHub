# Python Code

```python


class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        """
        Finds and returns a duplicate number in the given list of integers.

        Args:
            nums (List[int]): List of integers.

        Returns:
            int: The duplicate number found in the list.

        """
        index = 0
        
        # Iterate through the list to put each number in its correct position
        while index < len(nums):
            # Check if the current number is in its correct position
            if nums[index] != nums[nums[index] - 1]:
                # Swap the numbers to put them in their correct positions
                swap_index = nums[index] - 1
                nums[index], nums[swap_index] = nums[swap_index], nums[index]
            else:
                # Move to the next number if it is already in its correct position
                index += 1
        
        # Find the duplicate number by checking if each number is in its correct position
        for i in range(len(nums)):
            if nums[i] != i+1:
                return nums[i]

```

**Time Complexity**
- The time complexity of this solution is O(n), where n is the length of the input list nums

**Space Complexity**
- The space complexity is O(1) since we are not using any additional data structures that grow with the input size.
