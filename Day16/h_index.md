
# Description
[ H-Index](https://leetcode.com/problems/h-index/)

Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper, return the researcher's h-index.

According to the definition of h-index on Wikipedia: The h-index is defined as the maximum value of h such that the given researcher has published at least h papers that have each been cited at least h times.

# Note
- Could be done by counting sort O(n)

# Solution
## Solution 1

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        # sort citation 
        # guess for hIndex: let's say it's k 
        # check if citations[n-1-k]>=k
        citations.sort()
        n = len(citations)
   
        k = min(n, citations[n-1])
        max_h = 0
        if n == 1: 
            return k
    
        for i in range (1, k+1):
            if citations[n-i]>=i: 
                max_h= max(max_h, i)
        return max_h
```


