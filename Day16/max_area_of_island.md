# Description
Max Area of Island
https://leetcode.com/problems/max-area-of-island/description/



```python
from collections import deque
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        # bfs on every cell - keep expanding while can
        # store max area
        offsets = [(-1, 0), (1, 0), (0, -1), (0, 1)] 
        row, col = len(grid), len(grid[0])
        def bfs(r, c, q):
            area = 0
            q.append((r, c))

            while len(q)> 0: 
                (x, y) = q.pop()
                if grid[x][y] != -1: 
                    area+=1
                    grid[x][y] = -1
                    for (xo, yo) in offsets:
                        nx = x+ xo
                        ny = y+yo
                        if 0<= nx <row and 0<=ny<col and grid[nx][ny] == 1: 
                            q.append((nx, ny))
            return area

        max_area =0
        q = deque()
        for r in range (row): 
            for c in range (col):
                if grid[r][c] == 1:
                    area = bfs(r, c, q)
                    max_area = max(max_area, area)
        return max_area
```