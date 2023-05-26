# Python Code

```python

class Solution:
    def findPairs(self, A: List[int], B: int) -> int:
        i = 0
        j = 0
        result = 0
        A.sort()  # Sort the array A in ascending order

        while j < len(A) and i < len(A):
            if i == j:
                j += 1
                continue  # Skip the case where i and j point to the same index

            difference = A[j] - A[i]  # Calculate the difference between A[j] and A[i]

            if difference < B:
                j += 1
                continue  # Increment j if difference is less than B

            if difference > B:
                i += 1
                continue  # Increment i if difference is greater than B

            result += 1  # Increment the result count for each unique k-diff pair
            x = A[i]
            y = A[j]

            while i < len(A) and A[i] == x:
                i += 1  # Iterate over duplicate values of A[i]

            while j < len(A) and A[j] == y:
                j += 1  # Iterate over duplicate values of A[j]

        return result  # Return the final count of unique k-diff pairs



```


**Time Complexity**
- The code has a time complexity of O(n log n) due to the initial sorting of the array A, where n is the size of the input array. The while loop iterates at most n times, and the inner while loops iterate over duplicate values, so they don't contribute to the overall time complexity.
**Space Complexity**
- The space complexity of the code is O(1) since it uses a constant amount of extra space to store the variables and doesn't rely on any additional data structures proportional to the input size.
