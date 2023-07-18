# Python Code

```python


class Solution:

	def largestRectangleArea(self, A):

		nsl = []; nsr = [];
		stack = deque([]);

		for i in range(len(A)):

			while stack and A[stack[-1]] >= A[i]:
				stack.pop();
			if not stack:
				nsl.append(-1);
			else:
				nsl.append(stack[-1]);
			stack.append(i);

		stack = deque([]);

		for i in range(len(A)-1,-1,-1):

			while stack and A[stack[-1]] >= A[i]:
				stack.pop();
			if not stack:
				nsr.append(len(A));
			else:
				nsr.append(stack[-1]);
			stack.append(i);

		nsr = nsr[::-1];
		max_area = 0;print(nsl,nsr)
        
		for i in range(len(A)):

			width = nsr[i]-nsl[i]-1;
			curr_area = A[i]*width;

			max_area = max(max_area,curr_area);
		
		return max_area;



```

### Time Complexity
- O(N), where N is the length of the input array A. The function performs two passes over the array, one from left to right and another from right to left. In each pass, the while loop iterates at most N times. Therefore, the overall time complexity is linear with respect to the size of the input array.

- ### Space Complexity
- O(N), where N is the length of the input array A. The function uses two additional arrays, nsl and nsr, each of length N to store the indices of the next smaller elements to the left and right, respectively. Additionally, a stack is used to track the indices, which can have a maximum size of N in the worst case. Hence, the space complexity is linear with respect to the size of the input array.

# C++ Code
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();

        int result = 0;
        stack<int> st;
        vector<int> left(n,-1);
        vector<int> right(n,n);

        for(int i=0;i<n;i++){   //(left->NSL index)(monotonically increasing)
            while(st.size() && heights[st.top()] >= heights[i]){
                st.pop();
            }
            if(!st.empty()){
                left[i] = st.top();
            }
            st.push(i);
        }

        while(!st.empty()){ //empty the stack
            st.pop();
        }

        for(int i=0;i<n;i++){   //(right->NSR index)(monotonically increasing)
            while(st.size() && heights[st.top()] > heights[i]){
                right[st.top()] = i;
                st.pop();
            }
            st.push(i);
        }

        for(int i=0;i<n;i++){
            result = max(result,heights[i]*(right[i]-left[i]-1));
        }
        
        return result;
    }
};
```
