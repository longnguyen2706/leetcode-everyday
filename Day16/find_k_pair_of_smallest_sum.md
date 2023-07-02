
# Description
[Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums//)

You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.

Define a pair (u, v) which consists of one element from the first array and one element from the second array.

Return the k pairs (u1, v1), (u2, v2), ..., (uk, vk) with the smallest sums.

# Note
- Key thing is we not add every pair into Priority Queue, but just some pairs, then when we pop a pair out, add the next pair in 


# Solution
## Solution 1

```python
from queue import PriorityQueue

class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        m, n = len(nums1), len(nums2)
        i, j = 0, 0
        r = []
        k = min(m*n, k)
   
        pq= PriorityQueue()
        s = set()
        for i in range (m):
            pq.put((nums1[i]+ nums2[0], i,0))
            
        for j in range (n):
            pq.put((nums2[j]+ nums1[0], 0, j))
        
        while k>0:
            val, i, j = pq.get()
            # print (i, j, pq.qsize())
            if (i, j) not in s: 
                r.append([nums1[i], nums2[j]])
                s.add((i,j))
                # s.add((nums2[j], nums1[j]))
                k-=1
            
                if i+1< m and (i+1, j) not in s: 
                    pq.put((nums1[i+1]+ nums2[j], i+1, j))
                    # s.add((i+1, j))
                if j+1<n and (i, j+1) not in s: 
                    pq.put((nums1[i]+ nums2[j+1], i, j+1))
                    # s.add((i, j+1))
          
        return r
```


