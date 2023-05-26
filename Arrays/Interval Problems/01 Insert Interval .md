# Python Code

```python

class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        result = []
        intervals.sort()  # Sort intervals based on the start time
        
        for i in range(len(intervals)):
            if newInterval[1] < intervals[i][0]:
                # If the end time of newInterval is smaller than the start time of the current interval,
                # it means newInterval is non-overlapping and should be inserted here
                result.append(newInterval)
                result.extend(intervals[i:])
                return result
            
            elif newInterval[0] > intervals[i][1]:
                # If the start time of newInterval is greater than the end time of the current interval,
                # it means newInterval is non-overlapping and should be added to the result as is
                result.append(intervals[i])
            
            else:
                # If there is an overlap between newInterval and the current interval,
                # update the start and end time of newInterval by taking the minimum start time
                # and maximum end time between the two intervals
                newInterval[0] = min(newInterval[0], intervals[i][0])
                newInterval[1] = max(newInterval[1], intervals[i][1])
        
        # Add the final merged or non-overlapping newInterval to the result
        result.append(newInterval)
        
        return result


```

**Time Complexity**
- Sorting: The sort() function used on the intervals list has a time complexity of O(N log N), where N is the number of intervals. This is because the function uses an efficient sorting algorithm, typically based on comparison-based sorting like Merge Sort or Quick Sort.
- Iterating through intervals: The code then iterates through the sorted intervals once, which takes linear time O(N).

**Space Complexity**
- Output List: The result list is used to store the merged intervals. In the worst case, if there are no overlapping intervals, the output list can contain all the intervals, resulting in O(N) space.
- Sorting: The sort() function typically performs an in-place sort, which means it doesn't require additional space beyond the input list. Hence, the sorting operation doesn't contribute to the space complexity.
