# Description
[Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/description/)

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.

# Note
Time - 25mins - not optimal space

# Solution
## Solution 1
```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # since we cannot use additional memory, we need to find a smart way to 
        # diff the original 0 and every other 0 that introduced by us 
        # we will do in 2 pass: scan for 0 (1st), then set row/ col 0 (2nd)
        # also, we dont want to loop through every cell in row/ col in 1st (will take O(m+n)), so we just set the first cell in row/ col only

        row, col = len(matrix), len(matrix[0])
        cords = set()
        for r in range (row):
            for c in range (col): 
                if matrix[r][c] == 0: 
                   cords.add((-1, c)) # need to mark as -1 to diff from the original 0
                   cords.add((r, -1)) # need to mark as -1 to diff from the original 0
        # print (cords)
        for r in range(row):
            for c in range (col):
                if (-1, c) in cords or (r, -1) in cords:
                    matrix[r][c] = 0

    
```

# Solution 2
Optimal space - using iscol0 and isrow0 to mark if the first row and col is 0 

```python
def setZeroes(self, matrix: List[List[int]]) -> None:
        row, col = len(matrix), len(matrix[0])
        isrow0, iscol0 = False, False

        for r in range(row):
            if matrix[r][0] == 0:
                iscol0 = True 
        
        for c in range(col):
            if matrix[0][c] == 0: 
                isrow0 = True

        for r in range(1, row):
            for c in range(1, col): 
                if matrix[r][c] ==0:
                    matrix[r][0] = 0
                    matrix[0][c] = 0 
        
        # update the matrix
        for r in range (1, row):
            for c in range (1, col):
                if matrix[r][0] == 0 or matrix[0][c] == 0: 
                    matrix[r][c] = 0 
        if isrow0: 
            for c in range (0, col):
                matrix[0][c] = 0

        if iscol0: 
            for r in range (0, row):
                matrix[r][0] = 0
```