# Description
[Balanced Binary Tree](https://leetcode.com/problems/search-a-2d-matrix/description/)

Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.
# Note


# Solution
## Solution 1

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        # find the pivot. we will have left, pivot, right array 
        # min = min (right[0], left[0]); right and left are both increasing

        # binary search 
        n = len(nums)
        lo, hi = 0, n-1
        mid =0
         if nums[0]<nums[hi]: 
            return nums[0]
        while lo<hi: 
            mid = lo+ (hi-lo+1)//2
            if nums[mid-1]> nums[mid]:
                return nums[mid]
            if nums[mid]>nums[lo]:
                lo = mid
            else: 
                hi = mid -1
        return min(nums[lo], nums[mid])
```

## Solution 2

```python
        # binary search 
        n = len(nums)
        lo, hi = 0, n-1
        mid =0
        if nums[0]<nums[hi]: 
            return nums[0]
        while lo<hi: 
            mid = lo+ (hi-lo)//2
            # do not use nums[mid]>nums[lo] because it will fail
            # when lo==mid (ard found pivot, and we keep increasing low since the subarray is sorted and ascending, resulting in lo =hi)
            if nums[mid]>nums[hi]:  
                lo = mid+1
            else: 
                hi = mid
        return nums[lo]
```