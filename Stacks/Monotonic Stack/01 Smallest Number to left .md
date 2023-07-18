# Java Code

```java

import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

class Solution {
    /**
     * Returns a list of the previous smaller elements for each element in the array.
     *
     * @param n The size of the input array.
     * @param a The input array of integers.
     * @return The list of previous smaller elements.
     */
    static List<Integer> leftSmaller(int n, int[] a) {
        Stack<Integer> monoStack = new Stack<>();
        List<Integer> result = new ArrayList<>();

        // Iterate over the array elements
        for (int i = 0; i < n; i++) {
            // Remove elements from stack greater than or equal to current element
            while (!monoStack.isEmpty() && monoStack.peek() >= a[i]) {
                monoStack.pop();
            }

            // If stack is empty, there is no previous smaller element
            if (monoStack.isEmpty()) {
                result.add(-1);
            } else {
                // Add the top element of stack as the previous smaller element
                result.add(monoStack.peek());
            }

            // Push the current element to the stack
            monoStack.push(a[i]);
        }

        return result;
    }
}


```

### Time Complexity
- The time complexity of the leftSmaller method in the given code is O(n), where n is the size of the input array a. This is because the method iterates over the array once, performing stack operations for each element.

### Space Complexity
- The space complexity of the method is O(n), where n is the size of the input array a. This is due to the space used by the monoStack stack and the result list. In the worst case, the stack can store all the elements of the array if they are in non-decreasing order, resulting in O(n) space usage.

# C++ Code
```cpp
class Solution {
public:
    vector<int> NSL(vector<int> &v) {
        stack<int> st;
        vector<int> result(v.size(), -1);
        
        for(int i=0;i<v.size();i++){
            while(st.size() && st.top() >= v[i]){
                st.pop();
            }
            if(!st.empty()){
                result[i] = st.top();
            }
            st.push(v[i]);
        }

        return result;
    }
};
```
