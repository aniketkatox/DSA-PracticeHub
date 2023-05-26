# Python Code

```python

class Solution:
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        left, right = 0, len(nums) - 1  # Initialize left and right pointers
            
        while left < right:
            # Check if the sum of the elements at left and right pointers is less than the target
            if nums[left] + nums[right] < target:
                left += 1  # Move the left pointer to the right
                    
            # Check if the sum of the elements at left and right pointers is greater than the target
            elif nums[left] + nums[right] > target:
                right -= 1  # Move the right pointer to the left
                    
            else:
                return [left + 1, right + 1]  # Return the indices (1-based) of the two numbers that sum up to the target



```

**Time Complexity**
- The time complexity of this solution is O(n), where n is the length of the nums list.

**Space Complexity**
- The space complexity is O(1) since the algorithm do not uses a constant amount of extra space.
