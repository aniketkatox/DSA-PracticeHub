# Python code

```python

class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        """
        Find all unique quadruplets in the array whose sum is equal to the target.

        Args:
            nums: The input array of integers.
            target: The target sum.

        Returns:
            A list of unique quadruplets whose sum is equal to the target.

        """

        nums.sort()
        results = []
        self.findNSum(nums, target, 4, [], results)
     
        return results
    
    def findNSum(self, nums, target, N, combination, results):
        """
        Helper function to find N-sum combinations.

        Args:
            nums: The input array of integers.
            target: The remaining target sum.
            N: The number of elements to form the sum.
            combination: The current combination of elements.
            results: The list to store the resulting combinations.

        """

        if len(nums) < N or N < 2: 
            return
        
        if N == 2: 
            # Base case: Find unique pairs whose sum is equal to the target
            two_sum_results = self.findTwoSum(nums, target)
            if two_sum_results != []:
                for pair in two_sum_results:
                    results.append(combination + pair)
        
        else: 
            # Recursive case: Fix one element and find (N-1)-sum combinations
            for i in range(len(nums) - N + 1):
                if nums[i] * N > target or nums[-1] * N < target: 
                    break
                if i == 0 or i > 0 and nums[i - 1] != nums[i]: 
                    self.findNSum(nums[i + 1:], target - nums[i], N - 1, combination + [nums[i]], results)
    
    
    def findTwoSum(self, nums: List[int], target: int) -> List[int]:
        """
        Find all unique pairs in the array whose sum is equal to the target.

        Args:
            nums: The input array of integers.
            target: The target sum.

        Returns:
            A list of unique pairs whose sum is equal to the target.

        """
        res = []
        left = 0
        right = len(nums) - 1 
        while left < right: 
            current_sum = nums[left] + nums[right] 

            if current_sum == target:
                res.append([nums[left], nums[right]])
                right -= 1
                left += 1
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while right > left and nums[right] == nums[right + 1]:
                    right -= 1
                                
            elif current_sum < target: 
                left += 1 
            else: 
                right -= 1
                                        
        return res


```

**Time complexity**
- The time complexity of the fourSum method depends on the number of combinations generated. In the worst case, it can be O(N^3), where N is the length of the nums array

**Space Complexity**
- The space complexity is O(N) for the resulting combinations stored in the results list.

