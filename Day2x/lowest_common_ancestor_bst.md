# Description
Lowest Common Ancestor of a Binary Search Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/


# Note 
Time taken: 17 mins
- Note that the time complexity in worst case is still O(N), if the tree is not balanced 

# Solution 
```python 
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        # since it is bst, we could find the path to p and q in log(n)
        # search for overlap: path_p & path_q: just use 2 pt until we cannot proceed further
        # let's say we found the LCA. any grand parent of p will be grand parent of q, since there is only 1 way to travese from root to LCA  
        # 0, 5 -> 6,2 , 0 ; 6,2, 4,5 -> the LCA is 2 
       
        def find_path(root, node, res): 
            # since node is in BST, there is no chance root is None
           
            res.append(root)
            if root == node: 
                return res
            if node.val<root.val: 
                find_path(root.left, node, res)
            else: 
                find_path(root.right, node, res)
            return None

        def print_nodes(nodes): 
            for node in nodes: 
                print(node.val, " ", end="")
            print()
        
        path_p, path_q = [], []
        find_path(root, p, path_p)
        find_path(root, q, path_q)
        # print_nodes (path_p)
        # print_nodes (path_q)
        i, j, lca = 0, 0, root
        while i<len(path_p) and j<len(path_q):
            if path_p[i] == path_q[j]:
                lca = path_p[i]
                i+=1
                j+=1
            else: 
                break
        return lca 
```

Recursive without additional memory 

```python 
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        p_val, q_val, pr_val = p.val, q.val, root.val
        if p_val>pr_val and q_val>pr_val: # both p and q are on right branch
            return self.lowestCommonAncestor(root.right, p, q)
        elif p_val<pr_val and q_val<pr_val: # both p and q are on left branch 
            return self.lowestCommonAncestor(root.left, p, q)
        else: 
            return root
```