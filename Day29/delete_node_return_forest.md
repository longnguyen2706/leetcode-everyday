# Description 
Delete Nodes And Return Forest
https://leetcode.com/problems/delete-nodes-and-return-forest/description/

# Note 
- Time taken: 19 mins, first submission 
- Key point:
    - You dont need create a new set of node, just use s_val and check every node.val if it is inside
    - You also dont need to keep track of parent and side of parent (left/right), just set the node to None is enough
    
# Solution 
```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def delNodes(self, root: Optional[TreeNode], to_delete: List[int]) -> List[TreeNode]:
        # loop through the tree to find the nodes to delete and add to a set -> O(n)
        # for each node in set -> add its children to candidates. add root node
        # candidates node that not in set is the result 
        # we also need to delete node connection: parent -> node_to_del -> child. parent.child = None
       
        def find_node(node, p_node, side, s_val, s_node):
            if node == None:
                return
            if node.val in s_val: 
                s_node[node] = (p_node, side) # map node -> (parent, left or right)
            find_node(node.left, node, "left", s_val, s_node) 
            find_node(node.right,node, "right", s_val, s_node)

        if root == None: 
            return []
       
        s_val = set(to_delete)
        s_node = dict()
        find_node(root, None, "left", s_val, s_node) # parent of root is None

        s_candidate = set([root]) # hold all candidate for new roots
        for node in s_node:
            if node.left:
                s_candidate.add(node.left)
            if node.right: 
                s_candidate.add(node.right)
            parent, side = s_node[node] # remove connection in original tree when delete node
            if parent: 
                if side == 'left':
                    parent.left = None 
                else: 
                    parent.right = None 
                
        res = []
        for node in s_candidate:
            if node not in s_node:
                res.append(node)
        return res
```