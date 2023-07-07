https://leetcode.com/problems/binary-tree-inorder-traversal/description/


```python
from collections import deque

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        # def recur(root, res): 
        #     if root == None: 
        #         return res
        #     recur(root.left, res)
        #     res.append(root.val)
        #     recur(root.right, res)
        #     return res
        
        # return recur(root, [])

        if root == None: 
            return []

        s = deque()
        res = []
        node = root
        while len(s)>0 or node != None:
            while node != None:
                s.append(node) 
                node = node.left
            node = s.pop()
            res.append(node.val)
            node = node.right
        return res
            
```