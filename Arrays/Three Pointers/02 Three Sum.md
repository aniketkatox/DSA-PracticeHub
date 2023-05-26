# Python code

```python

class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        
        result = []
        nums.sort() # By this it will be easy to skip over the elements
        
        for i in range(len(nums)-2): # This loop wil run only n-3
            
            
            if i > 0 and nums[i] == nums[i-1]: # It is the most intitutive condition 
                # we have found all the possible triplits with nums[i-1] and now if nums[i] == nums[i-1]: then it will just be repeatition
                continue
            
            # Reduce the problem to 2Sum by fixing one element "nums[i]".
            
            low,high = i+1,len(nums)-1
            
            while low < high:
                
                triplet_sum = nums[low] + nums[high] + nums[i] 
                # print(triplet_sum)
                if triplet_sum < 0: # since we want sum = 0 hence we need to increase our sum
                    low += 1
                
                if triplet_sum > 0:# since we want sum = 0 hence we need to decrease our sum
                    high -= 1
                
                if triplet_sum == 0: # we have the desired sum
                    # print(triplet_sum)
                    result.append([nums[i],nums[low],nums[high]])
                    
                    low  += 1
                    high -= 1
                    
                    while low < high and nums[low] == nums[low-1]: # we do not want the same element
                        low += 1                                   # bcz if nums[low] is same prev. then nums[high] will also be same to satisfy the relation 
                    while high > low and nums[high] == nums[high+1]:
                        high -= 1
        return result
                         

```

**Time Complexity**
- The time complexity of the threeSum method is O(n^2), where n is the length of the nums array. The outer loop runs for n-2 iterations, and the inner while loop runs in a two-pointer fashion, taking O(n) iterations in the worst case. Therefore, the overall time complexity is O(n^2).

**Space Complexity**
- The space complexity is O(1) since the algorithm doesn't use any extra space that grows with the input size. It only uses a constant amount of extra space to store the result list and some variables during the process.
