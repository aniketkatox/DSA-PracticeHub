# Java Code

```Java

class Solution {
    /**
     * Calculates the sum of min(b) for every subarray in the given array.
     *
     * @param arr The input array of integers.
     * @return The sum of min(b) for every subarray.
     */
    public int sumSubarrayMins(int[] arr) {
        int n = arr.length;
        int[] left = new int[n]; // to store the count of elements to the left of the current element that are greater than or equal to it
        int[] right = new int[n]; // to store the count of elements to the right of the current element that are greater than it
        Stack<Integer> monoStack = new Stack<>();
        int mod = (int) 1e9 + 7;
        long sum = 0;

        // Calculate the count of elements to the left of each element
        for (int i = 0; i < n; i++) {
            while (!monoStack.isEmpty() && arr[i] <= arr[monoStack.peek()]) {
                monoStack.pop();
            }
            left[i] = monoStack.isEmpty() ? i + 1 : i - monoStack.peek();
            monoStack.push(i);
        }

        monoStack.clear(); // clear the monoStack for reusing

        // Calculate the count of elements to the right of each element
        for (int i = n - 1; i >= 0; i--) {
            while (!monoStack.isEmpty() && arr[i] < arr[monoStack.peek()]) {
                monoStack.pop();
            }
            right[i] = monoStack.isEmpty() ? n - i : monoStack.peek() - i;
            monoStack.push(i);
        }

        // Calculate the sum of min(b) for every subarray
        for (int i = 0; i < n; i++) {
            sum = (sum + ((((long)(arr[i] * left[i])) % mod) * right[i]) % mod) % mod;
        }

        return (int)sum;
    }
}


```

### Time Complexity
- The time complexity of the sumSubarrayMins method is O(n), where n is the length of the input array arr.

The first loop iterates through the array once to calculate the count of elements to the left of each element. This loop has a linear time complexity of O(n).
The second loop iterates through the array once again to calculate the count of elements to the right of each element. This loop also has a linear time complexity of O(n).
The third loop calculates the sum of min(b) for every subarray by iterating through the array once more. This loop has a linear time complexity of O(n) as well.


### Space Complexity
- The space complexity of the method is O(n) as well.

The left and right arrays each require O(n) space to store the count of elements to the left and right of each element.
The monoStack stack can contain at most n elements in the worst case, requiring O(n) space.
Additionally, a few constant variables are used, which require O(1) space.
Hence, the total space complexity is O(n).
