# Python Code


```python

from collections import deque

class Solution:
    def maximalRectangle(self, matrix):
        if not matrix or not matrix[0]:
            return 0

        rows = len(matrix)
        cols = len(matrix[0])

        heights = [0] * cols
        max_area = 0

        for i in range(rows):
            for j in range(cols):
                if matrix[i][j] == '1':
                    heights[j] += 1
                else:
                    heights[j] = 0

            curr_area = self.largestRectangleArea(heights)
            max_area = max(max_area, curr_area)

        return max_area

    def largestRectangleArea(self, heights):
        nsl = self.nextSmallerLeft(heights)
        nsr = self.nextSmallerRight(heights)

        max_area = 0
        for i in range(len(heights)):
            width = nsr[i] - nsl[i] - 1
            curr_area = heights[i] * width
            max_area = max(max_area, curr_area)

        return max_area

    def nextSmallerLeft(self, heights):
        nsl = [-1]
        stack = deque([0])

        for i in range(1, len(heights)):
            while stack and heights[stack[-1]] >= heights[i]:
                stack.pop()

            if not stack:
                nsl.append(-1)
            else:
                nsl.append(stack[-1])

            stack.append(i)

        return nsl

    def nextSmallerRight(self, heights):
        nsr = [len(heights)]
        stack = deque([len(heights) - 1])

        for i in range(len(heights) - 2, -1, -1):
            while stack and heights[stack[-1]] >= heights[i]:
                stack.pop()

            if not stack:
                nsr.append(len(heights))
            else:
                nsr.append(stack[-1])

            stack.append(i)

        return nsr[::-1]


```


### Time Complexity
- overall time complexity of the code is O(rows * cols)

### Space Complexity
- overall space complexity is O(N), where N is the maximum of the number of columns or the length of the heights array.
