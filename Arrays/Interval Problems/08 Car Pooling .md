# Python Code

```python

import heapq

class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        # Sort the trips based on the pickup location
        trips.sort(key=lambda x: x[1])
        
        # Create a min heap to track trips based on their drop-off locations
        min_heap = []
        
        # Initialize a variable to keep track of the current number of passengers in the car
        current_capacity = 0
        
        # Iterate through each trip
        for trip in trips:
            # Get the number of passengers, pickup location, and drop-off location for the current trip
            num_passengers, pickup_loc, dropoff_loc = trip
            
            # Remove the completed trips from the min heap
            while min_heap and min_heap[0][0] <= pickup_loc:
                completed_trip = heapq.heappop(min_heap)
                current_capacity -= completed_trip[1]
            
            # Add the passengers from the current trip to the min heap
            heapq.heappush(min_heap, (dropoff_loc, num_passengers))
            
            # Update the current capacity by adding the number of passengers from the current trip
            current_capacity += num_passengers
            
            # Check if the current capacity exceeds the maximum capacity
            if current_capacity > capacity:
                return False
        
        return True


```

**Time complexity**
- The time complexity of this solution is O(n log n), where n is the number of trips. This is because we sort the trips based on their pickup locations, which takes O(n log n) time. The subsequent operations, such as removing completed trips from the min heap and adding new trips to the heap, each take O(log n) time. Therefore, the overall time complexity is dominated by the sorting step.

**Space complexity**
- The space complexity is O(n), where n is the number of trips. This is because we use a min heap to store the trips based on their drop-off locations. In the worst case, all trips can be stored in the min heap. Additionally, we use a few extra variables and data structures with constant space requirements. Thus, the space complexity is proportional to the number of trips.
