# Description 

# Note
Just bfs/ dfs to mark island. Loop through all cells as starting point to count island

# Solution
## Solution 1

DFS 

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        def dfs(g, r, c, m, n): 
            g[r][c] = "-1" # visited
            for o in offsets: 
                x, y = r+o[0], c+o[1]
                if 0<=x<m and 0<=y<n and g[x][y] == "1": 
                    dfs(g, x, y, m, n)
        
        m, n = len(grid), len(grid[0])
        offsets = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        
        res =0
        for r in range(m):
            for c in range(n):
                if grid[r][c] == "1": 
                    dfs(grid, r, c, m, n)
                    res +=1 
        # print(grid)
        return res
    

```

# Solution 2

BFS with level traversal

```python
from collections import deque
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:

        def bfs(q):
            while len(q)>0:
                k = len(q)
                while k> 0: 
                    (r, c) = q.popleft()
                    k-=1
                    for o in offsets: 
                        x, y = r+o[0], c +o[1]
                        if 0<=x<m and 0<=y<n and grid[x][y] == "1": 
                            grid[x][y] = "-1" # visited
                            q.append((x,y))

        m, n = len(grid), len(grid[0])
        offsets = [(-1, 0), (1, 0), (0, 1), (0, -1)]

        res = 0 
        q = deque()
        for r in range(m):
            for c in range(n):
                if grid[r][c] == "1":
                    q.append((r,c))
                    grid[r][c] = "-1"
                    bfs(q)
                    res+=1
        return res
```

# Solution 3

BFS without level travelsal

```python
 def numIslands(self, grid: List[List[str]]) -> int:
            def bfs(q):
                while len(q)>0:
                    (r, c) = q.popleft()
                    for o in offsets: 
                        x, y = r+o[0], c +o[1]
                        if 0<=x<m and 0<=y<n and grid[x][y] == "1": 
                            grid[x][y] = "-1" # visited
                            q.append((x,y))

            m, n = len(grid), len(grid[0])
            offsets = [(-1, 0), (1, 0), (0, 1), (0, -1)]

            res = 0 
            q = deque()
            for r in range(m):
                for c in range(n):
                    if grid[r][c] == "1":
                        q.append((r,c))
                        grid[r][c] = "-1"
                        bfs(q)
                        res+=1
            return res
```