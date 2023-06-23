# Java Code

```java


class Solution {
    /**
     * Calculates the number of days you have to wait after each day to get a warmer temperature.
     *
     * @param temperatures An array of temperatures.
     * @return An array of integers representing the number of days waited.
     */
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                result[prevIndex] = i - prevIndex;
            }
            stack.push(i);
        }

        return result;
    }
}


```

### Time Complexity
- The time complexity of the dailyTemperatures function is O(n), where n is the number of temperatures in the input array. This is because we iterate through the array once, and for each element, we perform operations that take constant time. The while loop inside the for loop runs in constant time on average, as each temperature index is pushed and popped from the stack at most once.

- ### Space Complexity
- The space complexity of the function is O(n) as well. This is because in the worst case, all the temperatures could be in non-decreasing order, causing the stack to store all the indices. Therefore, the stack can contain up to n elements, resulting in O(n) space complexity.
- 
