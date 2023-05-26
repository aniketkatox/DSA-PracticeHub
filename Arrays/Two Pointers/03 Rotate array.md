# Python Code

```python

from typing import List

class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Rotates the elements of the list nums to the right by k steps in-place.

        Args:
            nums (List[int]): The list of integers.
            k (int): The number of steps to rotate.

        Returns:
            None: The function modifies nums in-place.

        """

        n = len(nums)
        k = k % n

        nums = self.reverse(nums, 0, len(nums) - 1)
        nums = self.reverse(nums, 0, k - 1)
        nums = self.reverse(nums, k, n - 1)

    def reverse(self, nums: List[int], start: int, end: int) -> List[int]:
        """
        Reverses the elements in the list nums between the start and end indices.

        Args:
            nums (List[int]): The list of integers.
            start (int): The start index.
            end (int): The end index.

        Returns:
            List[int]: The reversed list.

        """

        while start < end:
            nums[start], nums[end] = nums[end], nums[start]
            start += 1
            end -= 1

        return nums


```

**Time Complexity**
- Time complexity is O(n) .The code reverses the entire list in the reverse function, which takes O(n) time, and performs a constant number of operations in the rotate function.Hence, the overall time complexity is linear, where n is the size of the input list.

**Space Complexity**
- Space complexity is O(1).The code modifies the input list nums in-place without using any additional space that scales with the input size.Therefore, the space complexity is constant
