# Description
[Longest Increasing Subsequence](https://leetcode.com/problems/meeting-rooms/description/)

Given an integer array nums, return the length of the longest strictly increasing 
subsequence.

# Note

# Solution 
## Solution 1
Using DP

```python 
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [1] * n
        maxLen = 0
        if n == 1: 
            return 1
       
        for i in range (1, n):
            # end = nums[i]
            for j in range (0, i):
                if nums[i]> nums[j]:
                    dp[i] = max(dp[i], 1+ dp[j])
            maxLen = max(maxLen, dp[i])
        # print (dp)
        return maxLen
```

## Solution 2
Using observation

```python

```