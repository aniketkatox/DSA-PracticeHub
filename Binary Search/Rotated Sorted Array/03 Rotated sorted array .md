# Python Code

```python 

class Solution:
    def findMin(self, nums):
        """
        Finds the minimum element in a rotated sorted array.

        Args:
            nums (List[int]): The rotated sorted array.

        Returns:
            int: The minimum element in the array.
        """
        low = 0
        n = len(nums)
        hi = n - 1
     
        while low <= hi:
            mid = (low + hi) // 2
            
            if nums[low] <= nums[mid] <= nums[hi]:
                # Array is sorted, return the minimum element at the lowest index
                return nums[low]
            
            left_neighbor = (mid + n - 1) % n  # Get the index of the left neighbor (circular)
            right_neighbor = (mid + 1) % n  # Get the index of the right neighbor (circular)
            
            if nums[left_neighbor] > nums[mid] < nums[right_neighbor]:
                # Found the minimum element
                return nums[mid]
            
            elif nums[low] <= nums[mid]:
                # Left side is sorted, discard the left side
                low = mid + 1
                
            elif nums[hi] > nums[mid]:
                # Right side is sorted, discard the right side
                hi = mid - 1


```

## Time Complexity
- The time complexity of the findMin method is O(log n) as it performs a binary search, dividing the search space in half at each step.

## Space Complexity
- The space complexity is O(1) as it uses a constant amount of additional space for variables low, hi, mid, left_neighbor, and right_neighbor.

