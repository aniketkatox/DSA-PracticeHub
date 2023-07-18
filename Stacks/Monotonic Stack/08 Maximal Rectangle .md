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


# C++ Code
```cpp
class Solution {
public:

    int mah(vector<int> temp){
        int n = temp.size();

        vector<int> left(n,-1);
        vector<int> right(n,n);
        stack<int> st;
        int maximum_area = INT_MIN;

        //NSL index(monotonically increasing)
        for(int i=0;i<n;i++){
            while(st.size() && temp[st.top()] >= temp[i]){
                st.pop();
            }
            if(!st.empty()){
                left[i] = st.top();
            }
            st.push(i);
        }

        while(st.size()){   //emptying the stack
            st.pop();
        }

        //NSR index(monotonically increasing)
        for(int i=0;i<n;i++){
            while(st.size() && temp[st.top()] >= temp[i]){
                right[st.top()] = i;
                st.pop();
            }
            st.push(i);
        }

        for(int i=0;i<n;i++){
            maximum_area = max(maximum_area,temp[i]*(right[i]-left[i]-1));
        }

        return maximum_area;
    }

    int maximalRectangle(vector<vector<char>>& matrix) {
        int rows = matrix.size();
        int cols = matrix[0].size();

        vector<int> temp(cols,0);
        int maximum = INT_MIN;
        
        for(int i=0;i<rows;i++){
            for(int j=0;j<cols;j++){
                if(matrix[i][j] == '0'){
                    temp[j] = 0;
                }
                else{
                    temp[j] = temp[j]+(matrix[i][j]-'0');
                }
            }
            maximum = max(maximum,mah(temp));
        }

        return maximum;
    }
};
```
