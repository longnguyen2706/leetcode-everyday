
# Description
[Permutations](https://leetcode.com/problems/permutations/)

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

# Note



# Solution
## Solution 1
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        def backtrack(idx):
            if len(l) == n: 
                r.append(l[:])
                return

            for i in range (0, n):
                if nums[i] not in l:
                    l.append(nums[i])
                    backtrack(i+1)
                    l.remove(nums[i])

        r = []
        l = []
        backtrack (0)
        return r 

    # def permute(self, nums: List[int]) -> List[List[int]]:
    #     # expand the list from left to right 
    #     # add new number to ard build list from prev step: copy array and add the new number to pos 0, 1 ... n
    #     def recur(nums, last, lists): 
    #         if last ==0: 
    #             return [[nums[0]]]
    #         else: 
    #             r = []
    #             for l in lists: 
    #                 for i in range (0, len(l)+1):
    #                     ll = l.copy()
    #                     ll.insert(i, nums[last])
    #                     r.append(ll)
    #         return r
    #     r = []
    #     for i in range (0, len(nums)):
    #         r = recur (nums, i, r)
    #     return r
```