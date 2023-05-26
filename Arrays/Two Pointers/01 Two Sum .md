# Python Code

```python

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
        dx = {}  # Dictionary to store the complement values
        
        for idx, num in enumerate(nums):
            
            if target - num not in dx:  # Check if the complement is not already in the dictionary
                dx[num] = idx  # Add the number to the dictionary with its index as the value
            
            else:
                return [idx, dx[target - num]]  # If complement found, return the indices of the two numbers
        
        # If no pair is found, return an empty list or handle it according to the problem requirements
        return []


```

**Time Complexity**
- The time complexity of the twoSum function is O(n), where n is the number of elements in the nums list. The function iterates over the list once to build the dictionary dx and check for the complement value. Each dictionary lookup and insertion takes O(1) time on average.

**Space Complexity**
- The space complexity of the function is O(n) as well. The dictionary dx stores at most n elements, where each element represents a unique number from the nums list as a key and its corresponding index as the value.
