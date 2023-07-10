# Description

# Note 

# Solution
## Solution 1
```python
import heapq
class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        self.l = []
        self.k = k
        for num in nums: 
            self.add(num)
    
    def add(self, val: int) -> int:
        
        heapq.heappush(self.l, val)
        if len(self.l)> self.k: 
            heapq.heappop(self.l)
        # print (self.l)
        return self.l[0]
```