# Description
[Word Search II](https://leetcode.com/problems/word-search-ii/editorial/)

Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word. 

# Note
## Time spend: 
40 mins - got issue with run time error, due to search from the begining of the path instead of the last element in path.

## Common mistake
- Forget to mark visited cell as unvisited after dfs
    - Simply reinit the visited matrix after dfs on each cell in main for loop is not enough, we need to allow different path to use the same cell.
- Forget to remove last element in path: 
    - When we find a word, we need to remove the last element in path, otherwise, we will not be able to find other words that share the same prefix. 
    - For example, if we find "a" in path, we need to remove "a" from path, otherwise, we will not be able to find "ab" in the same path.
- Forget to continue to search even we find the word: 
    - Because there might be other words that share the same prefix (such as 'oa' and 'oaa')
- The code is not optimized yet, since everytime, we search from the begining of the path (should use the last element in path only)

## Tips 
- When implement Trie, we can use TrieNode.word to store the word (so no need to keep track of path when doing dfs)
- We dont need to implent Trie Search and Prefix method, as we can do it in DFS 
- We can use the board -> set `board[r][c] = '#'` to mark visited cell, instead of using a visited matrix.
# Solution
## My Solution 
Got time limit exceeded due to non optimize trie search. 
```python
```python
class TrieNode: 
    def __init__(self):
        self.children = [None] * 26
        self.is_leaf = False
    
    def add_word(self, word):
        cur = self
        for i in range(len(word)):
            idx = ord(word[i]) - ord('a')
            # print (idx, cur.children)
            if not cur.children[idx]:
                cur.children[idx] = TrieNode()
            cur = cur.children[idx]
        cur.is_leaf = True

    def is_pref(self, word):
        cur = self
        for i in range (len(word)):
            idx = ord(word[i]) - ord('a')
            if not cur.children[idx]:
                return False
            cur = cur.children[idx]
        return cur is not None 
    
    def is_word(self, word):
        cur = self
        for i in range (len(word)):
            idx = ord(word[i]) - ord('a')
            if not cur.children[idx]:
                return False
            cur = cur.children[idx]
        # print (cur.children, cur.is_leaf)
        return cur is not None and cur.is_leaf
            
class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        # build trie. 
        # dfs on each cell of board 
        # if path = prefix, continue
        # if path = word, return word
        
        def dfs(r, c, visited, root, path):
            # print (r, c, board[r][c], path)
            # visited
            if visited[r][c]:
                return
            
            visited[r][c] = True
            path += board[r][c]
            # print (path)
            
            # invalid path
            if not cur.is_pref(path): 
                path.pop()
                visited[r][c] = False
                return 
            if cur.is_word(path):
                result.add(to_word(path))
                # path.pop()
                # visited[r][c] = False
                # return
            
            for (i, j) in find_nei(r, c):
                dfs(i, j, visited, root, path)
            visited[r][c] = False
            path.pop()
            
                   
        def find_nei(r,c): 
            nei = []
            for (i,j) in offsets: 
                nr = r+i
                nc = c+j
                if nr>=0 and nr<row and nc>=0 and nc<col: 
                    nei.append((nr, nc))
            return nei

        def to_word(path):
            w = ''
            for c in path:
                w +=c
            return w
        
        root = TrieNode()
        for word in words: 
            root.add_word(word)
        
        row, col = len(board), len(board[0])
        offsets = [(-1, 0), (1, 0 ), (0, -1), (0, 1)]
        result = set()
        visited = [[False] * (col) for _ in range (row)]
        # for r in range(row):
        #     print (board[r])
        for r in range (row):
            for c in range(col):
                cur = root
                dfs(r, c, visited, cur, [])
                # print (visited)
        return list(result)
    
```
## Solution 1: 
```python
class TrieNode:
    def __init__(self):
        self.children = [None] * 26
        self.word = None # using word as the holding place for the word.
    
    def add_word(self, word):
        cur = self
        for i in range (len(word)):
            c = word[i]
            idx = ord(c) - ord('a')
            if not cur.children[idx]:
                cur.children[idx] = TrieNode()
            cur =  cur.children[idx]
        cur.word = word

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        def dfs(node, r, c):
            ch = board[r][c] # bk
            if ch == '#' or node.children[ord(ch) -ord('a')] == None: 
                return 

            node = node.children[ord(ch) -ord('a')]
            if node.word: 
                res.append(node.word)
                node.word = None # dedup, now we can not find this word again.
            board[r][c] = '#' # mark visited

            if (r > 0):
                dfs(node, r - 1, c)
            if (c > 0):
                dfs(node, r, c- 1)
            if (r < len(board) - 1):
                dfs(node, r+1, c)
            if (c < len(board[0]) - 1):
                dfs(node, r, c+1)
            board[r][c] = ch

        root = TrieNode()
        for w in words: 
            root.add_word(w)
        
        res = []
        for r in range (len(board)):
            for c in range (len(board[0])):
                dfs(root, r, c)
        return res
```