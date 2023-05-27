# Python code

```python

class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        points.sort(key=lambda x: x[0])  # Sort based on starting times
        end = float('-inf')  # Initialize end to negative infinity
        arrows = 0

        for start, curr_end in points:
            if start > end:  # Need a new arrow
                arrows += 1
                end = curr_end
            else:
                end = min(end, curr_end)

        return arrows


```

**Time Complexity**
- O(n log n), where n is the number of balloons. This is due to the sorting operation. The rest of the operations take O(n) time, resulting in a total time complexity of O(n log n).

**Space Complexity**
- The space complexity is O(1) as we only need a few variables to store the current ending time, the number of arrows, and the sorting is performed in-place on the given input array. 
