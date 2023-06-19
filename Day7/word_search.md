# Description
[Word Search] (https://leetcode.com/problems/word-search/)
Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

# Note

# Solution 
## 1st Solution
Got some edge case failed
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def dfs(idx, r, c, visited) -> bool:
                 
            # print (idx, word[idx], r, c, board[r][c], visited[r][c])
            if word[idx] != board[r][c]:
                return False
            visited[r][c] = True
            if idx == len(word)-1:
                return True
            neis = get_nei(row, col, r,c)
            # print (r, c, neis)
            for (i, j) in neis: 
                if not visited[i][j] and dfs(idx+1, i, j, visited):
                    return True
            
            return False

        def get_nei(row, col, r, c):
            nei = []
            for (i, j) in offset: 
                if r + i>=0 and r+i<row and c+j>=0 and c+j<col:
                    nei.append((r+i,c+j))
            return nei
        

        row, col  = len(board), len(board[0])
        offset = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        if row == 1 and col == 1: 
            return board[0][0] == word
        for r in range (row):
            for c  in range (col):
                visited = [[False] * col for _ in range(row)]
                if dfs(0, r, c, visited):
                    return True 
        
        return False 
                
```
## 2nd Solution
After doing word search ii. Still have TLE, due to a bad test case (user reported)
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def dfs(idx, r, c) -> bool:
            if idx >= len(word):
                return True    
            # print (idx, word[idx], r, c, board[r][c], visited[r][c])
            if board[r][c] == '#' or word[idx] != board[r][c]:
                return False
            
           
            if idx == len(word)-1:
                return True
            ch =board[r][c]
            board[r][c] = '#'
            neis = get_nei(row, col, r,c)
            # print (r, c, neis)
            for (i, j) in neis: 
                if dfs(idx+1, i, j):
                    return True
            board[r][c] = ch
            return False

        def get_nei(row, col, r, c):
            nei = []
            for (i, j) in offset: 
                if r + i>=0 and r+i<row and c+j>=0 and c+j<col:
                    nei.append((r+i,c+j))
            return nei
        

        row, col  = len(board), len(board[0])
        offset = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        if row == 1 and col == 1: 
            return board[0][0] == word
        for r in range (row):
            for c  in range (col):
                if dfs(0, r, c):
                    return True 
        
        return False 

```
