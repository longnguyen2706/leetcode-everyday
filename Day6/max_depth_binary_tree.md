# Description
[Max depth binary tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.  

# Note

# Solution
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        def recur(root):
            if not root:
                return 0
            return 1+ max(recur(root.left), recur(root.right))

        return recur(root)

```
