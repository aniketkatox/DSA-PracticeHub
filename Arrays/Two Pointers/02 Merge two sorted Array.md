# Python Code

```python

from typing import List

class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Merges two sorted lists nums1 and nums2 into nums1 in-place.

        Args:
            nums1 (List[int]): The first sorted list.
            m (int): The number of elements in nums1 (excluding the additional space for merging).
            nums2 (List[int]): The second sorted list.
            n (int): The number of elements in nums2.

        Returns:
            None: The function modifies nums1 in-place.

        """

        # Index variables for nums1, nums2, and the merged list
        i = m - 1
        j = n - 1
        k = m + n - 1

        while i >= 0 and j >= 0:
            # Compare the elements from nums1 and nums2
            if nums2[j] >= nums1[i]:
                # Append the larger element to the merged list from the right side
                nums1[k] = nums2[j]
                j -= 1
            else:
                nums1[k] = nums1[i]
                i -= 1
            k -= 1

        # If there are remaining elements in nums2, append them to the merged list
        if j >= 0:
            nums1[:k + 1] = nums2[:j + 1]


```


**Time complexity: O(m + n)**
- The code iterates over both input lists once, performing constant time operations in each iteration.
- Hence, the time complexity is linear, where m and n are the sizes of nums1 and nums2, respectively.

**Space complexity: O(1)**
- The code modifies nums1 in-place without using any additional space that scales with the input size.
- Therefore, the space complexity is constant.
