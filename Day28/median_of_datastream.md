# Description 

# Note 
- Key point: rebalance + push to left half if right half peek is smaller than number
- When using heapq, cannot just do list.pop(0) but need to use heapq.heappop(list) to get the smallest element

# Solution 
## Solution 1

```python
import heapq
class MedianFinder:
    # 2 heap: min heap for right half, max heap for left half 
    # need to keep these 2 even size, with favor of left half
    # add number: 
    # max(left)< min(right)
    # size left = right:  
    #   if right peek < number -> add right
    #   if right peak> number -> add left 
    # rebalance
     
    def __init__(self):
        self.left = []
        self.right = []

    def addNum(self, num: int) -> None:
        # favor left
        if len(self.left) == 0: 
            heapq.heappush(self.left, (-num, num))
            return

        # if left and right are equal
        (_, l_val) = self.left[0]
        if l_val>=num:
            heapq.heappush(self.left, (-num, num))
        else: 
            heapq.heappush(self.right, (num, num))
            
        # rebalance
        diff = len(self.left) - len(self.right)
        if diff == -2: 
            (_, val) = heapq.heappop(self.right)
            heapq.heappush(self.left, (-val, val))
        elif diff == 2: 
            (_, val) = heapq.heappop(self.left)
            heapq.heappush(self.right, (val, val))
      
    def findMedian(self) -> float:
        n = len(self.left)+ len(self.right)
        if n%2 == 0: 
            return (self.left[0][1]+ self.right[0][1])/2
        else: 
            return self.left[0][1] if len(self.left)> len(self.right) else self.right[0][1]
            


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```