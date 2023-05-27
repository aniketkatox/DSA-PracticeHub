# Python Code

```python


class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        """
        Finds and returns an array of integers that appear twice in the given array.

        Args:
            nums (List[int]): Input array of integers.

        Returns:
            List[int]: Array of integers that appear twice.

        """
        duplicates = []

        # Perform cyclic sort
        i = 0
        while i < len(nums):
            # Check if the current number is in its correct position
            if nums[i] != nums[nums[i] - 1]:
                # Swap the numbers to put them in their correct positions
                nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]
            else:
                i += 1

        # Find the duplicates
        for i in range(len(nums)):
            if nums[i] != i + 1:
                duplicates.append(nums[i])

        return duplicates


```

**Time Complexity**
- The time complexity of the solution is O(n) because the cyclic sort operation takes linear time, and the subsequent iteration to find the duplicates also takes linear time.

**Space Complexity**
- The space complexity of the solution is O(1) since we are using constant extra space to store the duplicates. We don't require any additional data structures that grow with the input size.

