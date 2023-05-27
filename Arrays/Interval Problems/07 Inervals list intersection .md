# Python Code


```python

class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        i, j = 0, 0  # Pointers to track current indices of firstList and secondList
        result = []  # List to store the intersection intervals
        
        while i < len(firstList) and j < len(secondList):
            start1, end1 = firstList[i]  # Interval from firstList
            start2, end2 = secondList[j]  # Interval from secondList
            
            # Check for intersection between the intervals
            if end1 < start2:
                # No intersection, move to the next interval in firstList
                i += 1
            elif end2 < start1:
                # No intersection, move to the next interval in secondList
                j += 1
            else:
                # Intersection exists, add it to the result list
                intersection_start = max(start1, start2)
                intersection_end = min(end1, end2)
                result.append([intersection_start, intersection_end])
                
                if end1 < end2:
                    # Interval from firstList ends first, move to the next interval in firstList
                    i += 1
                else:
                    # Interval from secondList ends first, move to the next interval in secondList
                    j += 1
        
        return result


```

**Time Complexity**
- The time complexity of the intervalIntersection function is O(N+M), where N is the length of the firstList and M is the length of the secondList. This is because the function iterates through both lists simultaneously, comparing intervals and finding intersections. In the worst case, it may need to iterate through all intervals in both lists.

**Space Complexity**
- The space complexity of the function is O(N+M) as well. This is because the function uses a result list to store the intersection intervals, and the size of the result list can be at most N+M if all intervals intersect. However, it is important to note that the result list does not contribute to additional space complexity as it is required in the output. Therefore, the overall space complexity is linear with respect to the input size.
