# Python Code

```python

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        
        intervals.sort()
        
        output = [intervals[0]]
        i = 1
        
        while i < len(intervals):
            
            if output[-1][1] >= intervals[i][0]: # compare last intervals y1 to current intervals x2
                               # lower limit will be x1 and upper limit will be max(y2,y1)
                output[-1]    = [output[-1][0],max(output[-1][1],intervals[i][1]) ] 
            
            else:# if not overlapping then simply append the interval
                 output.append(intervals[i])
            i = i + 1
        return output

```

**Time Complexity**

- Sorting: The code starts by sorting the intervals list, which has a time complexity of O(N log N), where N is the number of intervals. This is due to the efficient sorting algorithm used.
- Iterating through intervals: The code then iterates through the sorted intervals once, which takes linear time O(N).

**Space Complexity**

- Output List: The output list is used to store the merged intervals. In the worst case, where there are no overlapping intervals, the output list can contain all the intervals, resulting in O(N) space.
