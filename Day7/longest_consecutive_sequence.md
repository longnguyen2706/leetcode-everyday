# Description
[Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

# Note
- Time taken: < 10 mins


# Solution
## 1st Solution
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        def cal_left(n):
            if n not in left:
                return 0
            if left[n] > 0: # memoization
                return left[n]
            left[n] = 1+ cal_left(n-1)
            return left[n]

        def cal_right(n):
            if n not in right:
                return 0
            if right[n] > 0:
                return right[n]
            right[n] =  1+ cal_right(n+1)
            return right[n]

        left = {} # left[i] =  how long consercutive to the left of i (i is largest)
        right = {}  # right[i] =  how long consercutive to the right of i (i is smallest)
        for n in nums: 
            left[n] = 0
            right[n] = 0

        maxLen = 0 
        for n in nums: 
            maxLen = max(maxLen, cal_left(n), cal_right(n))
        # print ("left", left)
        # print ("right", right)
        return maxLen
    ```
## 2nd Solution
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        num_set = set(nums)
        max_len = 0 

        for n in num_set: 
            # will prevent calculating from the middle number in consecutive sequence. only the smallest number will execute
            if n-1 not in num_set: 
                cur = n 
                cur_streak = 1 

                while cur+1 in s:
                    cur +=1
                    cur_streak+=1
                max_len = max(cur_streak, max_len)
        return max_len

```

