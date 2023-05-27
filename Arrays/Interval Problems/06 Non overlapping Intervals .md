# Python Code

```python


class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key=lambda x: x[0])  # Sort based on starting times
        end = float('-inf')  # Initialize end to negative infinity
        removals = 0

        for start, end_curr in intervals:
            if start < end:  # Overlap with previous interval
                removals += 1
                end = min(end, end_curr) # as we will remove the interval
            else: # with minimum end time so that it does not overlap with upcoming intervals.
                end = end_curr

        return removals


```

**Time Complexity**
- The time complexity of this solution is O(n log n), where n is the number of intervals. This is due to the sorting operation. The rest of the operations take O(n) time, resulting in a total time complexity of O(n log n).

**Space Complexity**
- The space complexity is O(1) as we only need a few variables to store the current ending time, the number of removals, and the sorting is performed in-place on the given input array.
