# Python Code

```python

class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Sorts the array containing 0, 1, and 2 in-place in ascending order.

        Args:
            nums (List[int]): List of integers containing 0, 1, and 2.

        Returns:
            None. The array is modified in-place.
        """

        low, mid, high = 0, 0, len(nums) - 1
        
        # Use three pointers: low, mid, and high
        # Move mid pointer to traverse the array
        # Swap elements to their correct positions based on their values
        # 0 is moved to the beginning, 2 is moved to the end, and 1 stays in the middle
        while mid <= high:
            if nums[mid] == 0:
                self.swap(nums, low, mid)
                low += 1
                mid += 1  # Since the current element is now 0 and in its correct position
            elif nums[mid] == 2:
                self.swap(nums, mid, high)
                high -= 1
                # Don't increment mid as we need to process the swapped element
            else:
                mid += 1  # Move mid pointer when it points to 1
            
    def swap(self, nums, id1, id2):
        # Swaps the elements at the given indices in the array
        nums[id1], nums[id2] = nums[id2], nums[id1]


```

**Time Complexity**
- The time complexity of the sortColors method is O(n), where n is the length of the nums array. The algorithm traverses the array once, and each traversal operation takes constant time.

**Space Complexity**
- The space complexity is O(1) because the algorithm sorts the array in-place without using any additional data structures that grow with the input size. It uses only a constant amount of extra space to store the three pointers (low, mid, high) and temporary variables during swapping.
