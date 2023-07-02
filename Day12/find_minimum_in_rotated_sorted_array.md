# Description
[Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)


Given a binary tree, determine if it is 
height-balanced.

# Note


# Solution
## Solution 1

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        if root is None: 
            return  True
        # balanced if left height and right height diff less than 1
        height, is_valid = self.find_height(root)
        return is_valid

    def find_height(self, root):
        if root is None: 
            return 0, True
            
        left_height, left_valid =self.find_height(root.left)
        right_height, right_valid = self.find_height(root.right)    
        is_valid = left_valid and right_valid and abs(left_height-right_height)<=1

        return 1+ max(left_height, right_height), is_valid
```




