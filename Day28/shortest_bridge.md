# Description 

# Note

# Solution
## Solution 1
```python
from collections import deque
class Solution:
    def shortestBridge(self, grid: List[List[int]]) -> int:
        # find the 2 island, mark cell as 1 and 2 
        # for every cell with 1, bfs with level to find when it touch 2 
        offsets = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        m, n = len(grid), len(grid[0])
      
        def bfs1(q): 
            while len(q)> 0: 
                k = len(q)
                while k> 0: 
                    (r, c) = q.popleft()  
                    k-=1

                    for o in offsets: 
                        x, y= r+o[0], c+o[1]
                        if 0<=x<m and 0<=y<n and grid[x][y] == 1:
                            grid[x][y] = -1 # mark red
                            q.append((x, y))
        def bfs2(q):
            lvl = 10000000
            while len(q)> 0: 
                k = len(q)
                while k>0:
                    (r, c, l) = q.popleft()
                    k-=1
                    lvl = l

                    for o in offsets: 
                        x, y= r+o[0], c+o[1]

                        if 0<=x<m and 0<=y<n:
                            if grid[x][y] == 1: 
                                return l
                            
                            if grid[x][y] == 0:
                                grid[x][y] = 2 # mark blue. cannot mark as 1 since it will messed up
                                q.append((x, y, l+1))
            return lvl
        
        q = deque()
        found = False
        for r in range (m):
            for c in range (n):
                if grid[r][c] == 1 and not found: 
                    q.append((r, c))
                    grid[r][c] = -1
                    found = True # break is not enough, need to break out of 2 loops, so need found boolean
                    # print(q)
                    break
        bfs1 (q)
        # print(grid)
     
        lvl = 1000000000
        q = deque()
        for r in range (m):
            for c in range(n): 
                if grid[r][c] == -1: 
                    q.append((r, c, 0)) # keypoint is to add all -1 to the queue and do bfs level by level. otherwise, when doing bfs with some -1 and mark 0 as visited, some -1 wont be able to expand
        return bfs2(q)


```