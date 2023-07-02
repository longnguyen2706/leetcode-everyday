# Description
[Word Ladder](https://leetcode.com/problems/word-ladder/)

A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that:

Every adjacent pair of words differs by a single letter.
Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
sk == endWord
Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

# Note

# Solution
## Solution 1

```python
class Solution:
    def ladderLength(self, bw: str, ew: str, wl: List[str]) -> int:
        def build_adj():
            n = len(wl)
            adj = [[] for i in range (n+1)] # 0 -> begin word, n -> endWord  
            
            for i in range (n): 
                for j in range(i+1,n): 
                    if is_adj(wl[i], wl[j]):
                        adj[i+1].append(j+1)
                        adj[j+1].append(i+1)

            for i in range(n): # add bw to graph
                if is_adj(bw, wl[i]):
                    adj[0].append(i+1)
                    adj[i+1].append(0)
              
            return adj

        def is_adj(w1, w2):
            catch_diff= False
            i =0
            while i< len(w1):
                if w1[i] != w2[i]:
                # we need to have every thing same from now on
                    if catch_diff: 
                        return False
                    catch_diff=True
                i+=1

            return True
        
        n = len(wl)
        # find ew idx
        target_idx = -1 
        for i in range(0, n):
            if wl[i] == ew:
                target_idx = i
                break
        if target_idx == -1: # invalid case, ew is not in wl
            return 0
        # print (target_idx)

        adj = build_adj()
        # print (adj)
    
        visited = [False] * (n +1)
        # do bfs
        q = collections.deque([0])
        path_len = 0
        while len(q)>0:
            k = len(q)
            path_len+=1
            while k >0: 
                # print (q)
                node = q.popleft()
                k-=1
             
                if not visited[node]:
                    visited[node] = True
                    for v in adj[node]: 
                        if v == target_idx+1: # found 
                            return path_len +1
                        if not visited[v]: 
                            q.append(v)
        
        return 0
```
