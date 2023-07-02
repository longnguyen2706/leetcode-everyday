# Description
[Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/description/)

You are given an m x n integer matrix matrix with the following two properties:

Each row is sorted in non-decreasing order.
The first integer of each row is greater than the last integer of the previous row.
Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in O(log(m * n)) time complexity.

# Note
Time taken: 10 mins
 
Become basic after using binary search tips

# Solution
## Solution 1

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        # it is a binary search problem. 
        # here since first item of next row is larger than last row, if you write the matrix to an array, it is sorted array len(m*n)
        def convert(idx):
            r = idx//col
            c = idx - r*col 
            return r, c
        
        row, col = len(matrix), len(matrix[0])
        lo, hi =0, row*col-1
        while lo<hi:
            mid = lo + (hi-lo+1)//2
            r, c = convert(mid)
            if matrix[r][c]>target:
                hi=mid-1
            else:
                lo = mid
        r, c= convert(lo)
        return True if matrix[r][c] == target else False 
```