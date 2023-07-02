
# Description
[Rotting Oranges
](https://leetcode.com/problems/rotting-oranges/)

You are given an m x n grid where each cell can have one of three values:

0 representing an empty cell,
1 representing a fresh orange, or
2 representing a rotten orange.
Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

# Note



# Solution
## Solution 1
```python
from collections import deque

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        # bfs. every layer is 1 min
        offsets = [(-1, 0), (1, 0), (0, 1), (0, -1 )]
        row, col = len(grid), len(grid[0])
     

        def bfs(q, fresh_orange):
            step = 0
            while len(q)>0:
                k = len(q)
                while k> 0:
                    (x, y, lvl) = q.popleft()
                    # print (x, y, lvl)
                    step =lvl
                    k-=1
                    step =min(step, lvl)
                    for ox, oy in offsets: 
                        nx =x + ox
                        ny = y+ oy
                        if 0<=nx<row and 0<=ny<col and grid[nx][ny] == 1:
                            fresh_orange-=1
                            grid[nx][ny] = 2 # mark as rotten
                            q.append((nx, ny, lvl+1))

            return step, fresh_orange
        
        
        q = deque()
        fresh_orange = 0
        for r in range (0, row): 
            for c in range (0, col): 
                if grid[r][c] == 2: # seed - rotten orange
                    q.append((r, c, 0))
                elif grid[r][c] == 1:
                    fresh_orange+=1 
        step, orange_count = bfs(q, fresh_orange) # keep track of fresh orange
       
        return step if orange_count == 0 else -1
```