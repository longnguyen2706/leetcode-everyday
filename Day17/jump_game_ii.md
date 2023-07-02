
# Description
[Jump Game II](https://leetcode.com/problems/jump-game-ii/)

You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

0 <= j <= nums[i] and
i + j < n
Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

# Note



# Solution
## Solution 1
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        # convert array to max reachable index arr
        # 2, 4, 3, 4, 5
        # 3, 5, 2, 4, 5
        # to jump to n-1, we need to jump to any cell that val = n-1
        # greedy means we need to jump to the first cell that val = n-1
        # then repeat, problem become find a way to jump to that cell 

        n = len(nums)
        if n == 1: 
            return 0

        reach = [0] * n
        for idx , num in enumerate(nums):
            reach[idx] = min(n-1, num+ idx)
    
        idx, count, maxreach = 0, 0, reach[0]
        while idx< n:
            if reach[idx] == n-1: 
                return count if idx == n-1 else count + 1
            m = maxreach
            while idx<=m:    
                maxreach = max(maxreach, reach[idx])
                idx+=1
            count+=1
            idx-=1

        return count
```