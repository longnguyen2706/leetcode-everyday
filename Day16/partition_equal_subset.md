Partition Equal Subset Sum

Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.


```python 
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        # need to find a subset that sum to half of total sum 
        # dp[]: boolean array, whether can find such sum 
        # dp[n] = dp[n-1][target]| dp[n-1][target-nums[n]]
        
        n = len(nums)
        target = 0
        for num in nums:
            target+= num
        if target %2 == 1:
            return False 
        target = target//2

        dp = [[False]*(target+1) for i in range (0, n+ 1)]
        dp[0][0] = True
        for t in range (0, target+1):
            for i in range(1, n+1):
                if t ==0: 
                    dp[i][t] =True
                    continue
                dp[i][t] = dp[i-1][t]
                if t>=nums[i-1]:
                    dp[i][t] |= dp[i-1][t-nums[i-1]]
        
        # for row in dp:
        #     print (row)
        return dp[n][target]
```