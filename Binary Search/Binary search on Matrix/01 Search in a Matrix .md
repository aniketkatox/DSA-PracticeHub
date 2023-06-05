# Python Code

```python 


class Solution:

   def searchMatrix(self, A, B):
       
       low  = 0;
       high = len(A)-1;
       
       row = None   
       
       while low <= high :
           
           mid = (low+high)//2;
           
           if A[mid][-1] == B:
               return 1
           
           if A[mid][-1] > B:
               row = mid;
               high = mid - 1;
           
           else:
               low = mid + 1;

       if row == None :
           return 0;
       
       low  = 0;
       high = len(A[0])-1;

       while low <= high:
           
           mid = (high+low)//2;

           if A[row][mid] == B:
               return 1;
           
           if A[row][mid] > B:
               high = mid - 1;
           
           else:
               low = mid + 1;
       
       return 0;


```

## Time Complexity
- The time complexity of the searchMatrix method is O(log(m) + log(n)), where m is the number of rows and n is the number of columns in the matrix. This is because the method performs two binary searches: one to find the target row based on the last column elements, and another to search for the target within the selected row. Each binary search has a time complexity of O(log(k)), where k is the number of elements in the search range.

## Space Complexity
- The space complexity of the searchMatrix method is O(1), as it only uses a constant amount of extra space for storing variables and performing the binary search operations. The input matrix is not modified, and no additional data structures are created that depend on the size of the input.

