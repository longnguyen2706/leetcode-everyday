# Description
[Combination sum](https://leetcode.com/problems/combination-sum/)

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

# Note

# Solution 
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = set()
        self.recur(candidates, target, [], res)
        return list(res) 

    def recur(self, c_arr, target, path, res):
        if target == 0: 
            path.sort()
            res.add(tuple(path))
            return
        for c in c_arr:
            if target>=c:
                self.recur(c_arr, target-c, path+[c], res)
                
```

