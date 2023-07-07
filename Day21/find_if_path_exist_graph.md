# Description
[Find if Path Exists in Graph
](https://leetcode.com/problems/find-if-path-exists-in-graph/description/)

There is a bi-directional graph with n vertices, where each vertex is labeled from 0 to n - 1 (inclusive). The edges in the graph are represented as a 2D integer array edges, where each edges[i] = [ui, vi] denotes a bi-directional edge between vertex ui and vertex vi. Every vertex pair is connected by at most one edge, and no vertex has an edge to itself.

You want to determine if there is a valid path that exists from vertex source to vertex destination.

Given edges and the integers n, source, and destination, return true if there is a valid path from source to destination, or false otherwise.

# Note
- Forgot how to use deque 
- Forgot how to init a 2D array (adj = [[] for i in range(n)] in this case)


# Solution
## Solution 1
```python
from collections import deque
class Solution:
    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        def bfs(edges, q, visited):
            while len(q)>0: 
                k = len(q)
                # print (q)
                while k>0:
                    node = q.popleft()
                    k-=1
                    for v in adj[node]:
                        if not visited[v]:
                            if v == destination: 
                                print (v, destination)
                                return True 
                            visited[v] = True
                            q.append(v)
            return False

        if source == destination: 
            return True 
                   
        q = deque()
        visited = [False] *n
        adj = [[] for i in range(n)]
        
        for e in edges: 
            # print (e, e[0], e[1])
            adj[e[0]].append(e[1])
            adj[e[1]].append(e[0])

        q.append(source)
        visited[source] = True 
        return bfs(edges, q, visited)
```

```python
from collections import deque
class Solution:
    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        def bfs(q, visited):
           while len(q)>0: 
            u = q.popleft()
            if u == destination: 
                return True 
            for v in adj[u]:
                if not visited[v]:
                    visited[v] = True
                    q.append(v)

            return False
                   
        q = deque()
        visited = [False] *n
        adj = [[] for i in range(n)]

        for e in edges: 
            adj[e[0]].append(e[1])
            adj[e[1]].append(e[0])

        q.append(source)
        visited[source] = True 
        return bfs(edges, q, visited)
```