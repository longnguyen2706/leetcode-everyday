# Description 
Detonate the Maximum Bombs

https://leetcode.com/problems/detonate-the-maximum-bombs/description/

# Note 
- Time taken: 12 mins, 1st trial, but not optimal
- After changing a bit, it reduces from O(n^3) to O(n^2). Building list of detonate bombs when bomb i detonates, we have a graph and can do BFS 

# Solution 
## Solution 1
O(n^3)
```python
from collections import deque

class Solution:
    def maximumDetonation(self, bombs: List[List[int]]) -> int:
        # bomb1 detonate bomb2 if d(c1, c2)<=r
        # keep a map of dist: ci -> cj
        # everytime a bomb detonate: check what other detonate bombs (O(n))? 

        def cal_dist(b1, b2): 
            return math.sqrt((b1[0]- b2[0]) **2 + (b1[1]- b2[1]) **2)

        def detonate(i): 
            res = 1
            q = deque()
            q.append(i)
            s = set([i])  
            while len(q)> 0: 
                idx = q.popleft()
       
                for j in range(n): 
                    if dist[idx][j]<= bombs[idx][2] and j not in s:  # radius
                        res+=1
                        s.add(j)
                        q.append(j)
            return res

        n = len(bombs)
        dist = [[0]*n for _ in range(n)]
        for i in range(n): 
            for j in range(n): 
                dist[i][j] = cal_dist(bombs[i], bombs[j])
        
        res = 0
        for i in range(n): 
            res = max(res, detonate(i))
        return res

```

## Solution 2
O(n^2)
```python
from collections import deque

class Solution:
    def maximumDetonation(self, bombs: List[List[int]]) -> int:
        # bomb1 detonate bomb2 if d(c1, c2)<=r
        # keep a map of dist: ci -> cj
        # everytime a bomb detonate: check what other detonate bombs (O(n))? 

        def cal_dist(b1, b2): 
            return math.sqrt((b1[0]- b2[0]) **2 + (b1[1]- b2[1]) **2)

        def detonate(idx): # now it becomes bfs
            res = 1
            q = deque()
            q.append(idx)
            vis = set([idx])
            while len(q)> 0: 
                i =  q.popleft()
                for j in det[i]:
                    if j not in vis: 
                        vis.add(j)
                        res +=1
                        q.append(j)
            return res
           

        n = len(bombs)
        det = [[None] for _ in range(n)] # list of detonate bombs if bomb i detonate
        for i in range(n): 
            det[i] = []
            for j in range(n): 
                if j == i: 
                    continue
                dist = cal_dist(bombs[i], bombs[j])
                if dist<= bombs[i][2]:
                    det[i].append(j)

        # if there is a map holding bomb i, list bomb will gone
        res = 0
        for i in range(n): 
            res = max(res, detonate(i))
        return res
```