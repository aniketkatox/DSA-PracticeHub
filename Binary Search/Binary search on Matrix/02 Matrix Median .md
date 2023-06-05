# Python Code

```python 


class Solution:
    def matrix_search(self, A, B):
        """
        Counts the number of elements in the matrix A that are less than B.

        Args:
            A (List[List[int]]): The input 2D matrix.
            B (int): The target value.

        Returns:
            int: The count of elements in A that are less than B.
        """
        num_ele = 0
        
        for row in range(len(A)):
            low = 0
            high = len(A[0]) - 1
            index = -1
            
            while low <= high:
                mid = (low + high) // 2
                
                if A[row][mid] < B:
                    index = mid
                    low = mid + 1
                else:
                    high = mid - 1
            
            num_ele += (index + 1)
        
        return num_ele

    def findMedian(self, A):
        """
        Finds the median value in the matrix A.

        Args:
            A (List[List[int]]): The input 2D matrix.

        Returns:
            int: The median value in A.
        """
        low = float('inf')
        for i in range(len(A)):
            low = min(low, A[i][0])

        high = float('-inf')
        for i in range(len(A)):
            high = max(high, A[i][-1])

        median = -1
        n = (len(A) * len(A[0])) // 2

        while low <= high:
            mid = low + (high - low) // 2
            ans = self.matrix_search(A, mid)

            if ans <= n:
                median = mid
                low = mid + 1
            if ans > n:
                high = mid - 1

        return median


```


## Time Complexity

- The time complexity of the matrix_search function is O(m * log(n)), where m is the number of rows in the matrix A and n is the number of columns. This is because for each row, a binary search is performed on the columns, which takes O(log(n)) time. Since this process is repeated for each row (m times), the overall time complexity is O(m * log(n)).

## Space Complexity

- The space complexity of both functions is O(1) because they use a constant amount of additional space, regardless of the size of the input matrix. They do not use any additional data structures that scale with the input size.
