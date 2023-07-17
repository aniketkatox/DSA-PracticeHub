# Java Code


```Java


class Solution
{
    //Function to find the next greater element for each element of the array.
    public static long[] nextLargerElement(long[] arr, int n) {
            long[] result = new long[n];
            Arrays.fill(result, -1); // Initialize all elements in result array to -1
            Stack<Integer> monoStack = new Stack<>(); // Store indices of elements in the monoStack
    
            for (int i = 0; i < n; i++) {
                // Check if the current element is greater than elements at indices stored in the monoStack
                while (!monoStack.isEmpty() && arr[i] > arr[monoStack.peek()]) {
                    int index = monoStack.pop();
                    result[index] = arr[i];
                }
                monoStack.push(i); // Push the current element index to the monoStack
            }
    
            return result;
        }
}

```

**Time Complexity**
- O(n)

**Space Complexity**
- O(n)

# C++ Code

```cpp
class Solution {
public:
    vector<int> NGR(vector<int> &v) {
        stack<int> st;
        vector<int> result(v.size(), -1);

        for (int i = 0; i < v.size(); i++) {
            while (!st.empty() && v[st.top()] <= v[i]) {
                result[st.top()] = v[i];
                st.pop();
            }
            st.push(i);
        }

        return result;
    }
};
```
