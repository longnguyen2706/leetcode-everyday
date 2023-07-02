# Description
[Interleaving String](https://leetcode.com/problems/interleaving-string/description/)

Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.

An interleaving of two strings s and t is a configuration where s and t are divided into n and m 
substrings
 respectively, such that:

s = s1 + s2 + ... + sn
t = t1 + t2 + ... + tm
|n - m| <= 1
The interleaving is s1 + t1 + s2 + t2 + s3 + t3 + ... or t1 + s1 + t2 + s2 + t3 + s3 + ...
Note: a + b is the concatenation of strings a and b.

# Note

# Solution
## Solution 1
2D DP
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        # dp[i][j] = dp[i-1][j] if take letter from s1
        # = dp[i][j-1] if take letter from s2
        # dp[m][n] needs to be true
        m, n = len(s1), len (s2)
        if m+n != len(s3):
            return False 
        if s1 == "":
            return s2 == s3
        if s2 == "":
            return s1 == s3
    
        dp = [[False] * (n+1) for _ in range(m+1)]
        for i in range (0, m+1):
            for j in range (0, n+1):
                if i ==0 and j ==0:
                    dp[i][j] = 1
                elif i ==0: 
                    dp[i][j] = dp[i][j-1] and s2[j-1] == s3[i+j-1]
                elif j ==0: 
                     dp[i][j] = dp[i-1][j] and s1[i-1] == s3[i+j-1]
                
                else:
                    if s3[i+j-1] == s1[i-1]:
                        dp[i][j] = dp[i][j] or dp[i-1][j]
                    if s3[i+j-1] == s2[j-1]:
                        dp[i][j] = dp[i][j] or dp[i][j-1]
        return dp[m][n]
```
