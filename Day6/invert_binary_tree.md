# Description
[Invert Tree](https://leetcode.com/problems/invert-binary-tree/)

Given the root of a binary tree, invert the tree, and return its root.

# Note

# Solution
```python
 def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        def recur(root):
            if not root: 
                return None 
            n1 = recur (root.left)
            n2 = recur (root.right)
            root.left = n2
            root.right = n1
            return root
        
        return recur(root)
```