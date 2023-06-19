# Description
[Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree)

You have a graph of n nodes labeled from 0 to n - 1. You are given an integer n and a list of edges where edges[i] = [ai, bi] indicates that there is an undirected edge between nodes ai and bi in the graph.

Return true if the edges of the given graph make up a valid tree, and false otherwise.

# Note
- Time taken: < 10 mins
- Need to do with Union Find (Disjoint Set)

# Solution
## 1st Solution
```python
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        def dfs(node):
            if visited[node]:
                return
            visited[node] = True 
            for v in adj[node]:
                dfs(v)
        
        # connected tree needs to have n-1 edges
        if not len(edges) == n-1: 
            return False

        # build adj list
        adj = [[] for _ in range (n)]
        for e in edges:
            adj[e[0]].append(e[1])
            adj[e[1]].append(e[0])

        visited = [False] * n
        dfs(0)
        # to be valid tree, all nodes need to be visited 
        for i in range (n):
            if not visited[i]:
                return False
        return True
    ```