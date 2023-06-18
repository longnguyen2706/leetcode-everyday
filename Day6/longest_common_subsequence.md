# Description
[LCS](https://leetcode.com/problems/longest-common-subsequence/)

Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

# Note

# Solution 
My solution - 2D DP - O(mn)
```python
class Solution:
    def longestCommonSubsequence(self, s: str, t: str) -> int:
        m, n = len(s), len(t)
        dp = [[0] * (n+1) for i in range(0, m+1)]
        # print (len(dp),  len(dp[0]))
        maxLen = 0
        for i in range (1, m+1):
            for j in range(1, n+1):
                if s[i-1] == t[j-1]:
                    # print (i, j, m, n)
                    dp[i][j] = dp[i-1][j-1] + 1
                    maxLen = max(maxLen, dp[i][j])
                else: 
                    dp[i][j] = max(dp[i][j-1], dp[i-1][j])

        # print(dp)
        return maxLen

```
