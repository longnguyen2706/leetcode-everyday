<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Description](#description)
- [Note](#note)
- [Solution](#solution)
  - [Solution 1: in place replace](#solution-1-in-place-replace)
  - [python](#python)
  - [java](#java)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Description
[Rotate image](https://leetcode.com/submissions/detail/969994326/)

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

# Note
There is another solution which flip row first


# Solution
## Solution 1: in place replace 
Key difficulty = range of inner loop (otherwise, the ard processed cell will be process again) 
## python
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """

        n = len(matrix)
        for i in range (0, n//2 + n%2):
            for j in range (0, n//2):
                temp = matrix[i][j]
                matrix[i][j] = matrix[n-1-j][i]
                matrix[n-1-j][i] = matrix[n-1-i][n-1-j]
                matrix[n-1-i][n-1-j] = matrix[j][n-1-i]
                matrix[j][n-1-i] = temp 
```

## java
```java
class Solution {
    public void rotate(int[][] matrix) {
       int n = matrix.length;
       // rotate layer by layer 
       // top -> right -> bottom -> left 
       // layer = [rl, rh, cl, ch]. terminate when rl >= rh, cl >= ch
        
        // for (int i = 0; i< n/2; i++){
        //     for (int j =i; j<=n/2; j++){
        //         rot(matrix, i, j, n-1-i);
        //     }
        // }
        for (int i =0; i<n/2; i++){
            for (int j =i; j<n-1-i; j++){
                rot(matrix, i, j, n-1);
            }
        }

        // for (int i =0; i<n; i++){
        //     System.out.println(Arrays.toString(matrix[i]));
        // }
    }

    private void rot(int[][] m, int r, int c, int h){
        int temp = m[r][c];
        m[r][c] = m[h-c][r];
        m[h-c][r] = m[h-r][h-c];
        m[h-r][h-c] = m[c][h-r];
        m[c][h-r] = temp;  
        // System.out.println(h-c + " " +r + ", " + (h-r) + " " + (h-c) + ", "  + c + " " + (h-r)); 
        // System.out.println("r: "+ r + " c: " + c + " h: " + h);
    }
}

```