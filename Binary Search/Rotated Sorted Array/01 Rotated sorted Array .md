# Python Code

```python 


class Solution:
    def getPivot(self, nums):
        """
        Finds the index of the pivot element in a rotated sorted array.

        Args:
            nums (List[int]): The rotated sorted array.

        Returns:
            int: The index of the pivot element.
        """
        low = 0
        high = len(nums) - 1

        while low <= high:
            mid = (low + high) // 2

            if nums[mid] >= nums[low] and nums[mid] <= nums[high]:
                # If the middle element is between the first and last element, it means the array is not rotated
                # The pivot element is at the lowest index (low)
                return low
            else:
                # In this case, nums[low] will always be greater than nums[high]
                if nums[mid] > nums[high]:
                    # Pivot is on the right side, discard the left side
                    low = mid + 1
                elif nums[mid] < nums[high]:
                    # Pivot is on the left side, discard the right side
                    high = mid

    def search(self, nums, target):
        """
        Searches for the target value in a rotated sorted array.

        Args:
            nums (List[int]): The rotated sorted array.
            target (int): The target value to search.

        Returns:
            int: The index of the target value if found, -1 otherwise.
        """
        ln = len(nums)
        minimum = float('inf')

        pivot = self.getPivot(nums)

        low = pivot
        high = pivot + ln - 1
        while low <= high:
            mid = (low + high) // 2
            middle = mid % ln
            if nums[middle] == target:
                # Found the target value
                return middle
            elif nums[middle] > target:
                # Target is smaller than the middle element, search in the left half
                high = mid - 1
            else:
                # Target is larger than the middle element, search in the right half
                low = mid + 1

        # Target value not found
        return -1


```

## Time Complexity
- The time complexity of the search function in the given code is O(log N), where N is the length of the input nums array. This is because the binary search algorithm is used to search for the target value, and in each iteration, the search space is reduced by half.

## Space Complexity
- The space complexity is O(1) because the code uses a constant amount of extra space to store variables such as low, high, pivot, mid, and middle. The space usage does not depend on the size of the input array.

