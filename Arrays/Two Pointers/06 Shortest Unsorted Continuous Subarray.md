# Python Code


```python

class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        """
        Finds the shortest subarray that, if sorted, would make the entire array sorted.

        Args:
            nums (List[int]): List of integers.

        Returns:
            int: Length of the shortest subarray.
        """
        min_num = float('inf')  # Initialize the minimum number
        max_num = float('-inf')  # Initialize the maximum number
        flag = False  # Flag to track if unsorted elements are found
        
        # Find the minimum number in the unsorted portion of the array
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                flag = True
            if flag:
                min_num = min(min_num, nums[i])
        
        if not flag:
            return 0  # Array is already sorted
        
        flag = False  # Reset the flag
        
        # Find the maximum number in the unsorted portion of the array
        for i in range(len(nums)-2, -1, -1):
            if nums[i] > nums[i+1]:
                flag = True
            if flag:
                max_num = max(max_num, nums[i])
        
        # Find the leftmost index of the subarray
        for i in range(len(nums)):
            if nums[i] > min_num:
                left = i
                break
        
        # Find the rightmost index of the subarray
        for i in range(len(nums)-1, -1, -1):
            if nums[i] < max_num:
                right = i
                break
        
        return right - left + 1


```

**Time complexity**
- The algorithm makes three passes through the given nums list, each with O(n) time complexity, where n is the length of the nums list. Therefore, the overall time complexity is O(n).

**Space complexity**
- The algorithm uses a constant amount of extra space, regardless of the input size. It does not require any additional data structures that grow with the input size. Hence, the space complexity is O(1).
