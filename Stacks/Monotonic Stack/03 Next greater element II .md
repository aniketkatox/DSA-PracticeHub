# Java Code

```java


class Solution {
    /**
     * Finds the next greater elements for each element in the given array.
     * The next greater element of an element is the nearest element on the right
     * which is greater than the current element.
     *
     * @param nums The input array of integers.
     * @return An array containing the next greater elements for each element in the input array.
     */
    public int[] nextGreaterElements(int[] nums) {
        Stack<Integer> monoStack = new Stack<>();
        int[] result = new int[nums.length];
        Arrays.fill(result, -1);

        for (int i = 2 * nums.length - 1; i >= 0; i--) {
            while (!monoStack.isEmpty() && nums[i % nums.length] >= nums[monoStack.peek()]) {
                monoStack.pop();
            }
            if (!monoStack.isEmpty()) {
                result[i % nums.length] = nums[monoStack.peek()];
            }
            monoStack.push(i % nums.length);
        }
        return result;
    }
}


```

### Time Complexity
- The for loop iterates 2N-1 times, where N is the length of the input array nums.
Each iteration of the loop takes constant time, as it performs stack operations and array element assignments.
Therefore, the overall time complexity is O(N).

### Space Complexity 
- The space complexity is determined by the extra space used by the monoStack stack and the result array.
The size of the stack can grow up to the maximum size of the input array nums, which is N.
The result array also has a length of N, storing the next greater elements for each element in nums.
Hence, the overall space complexity is O(N).

# C++ Code
```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n = nums.size();
        vector<int> result(n,-1);
        stack<int> st;

        for(int i=0;i<2*n;i++){
            while(st.size() && nums[st.top()] < nums[i%n]){
                result[st.top()] = nums[i%n];
                st.pop();
            }
            st.push(i%n);
        }

        return result;
    }
};
```
