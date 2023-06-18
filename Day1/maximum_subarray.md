# Description
[Maximum subarray   ](https://leetcode.com/problems/maximum-subarray/)

Given an integer array nums, find the subarray with the largest sum, and return its sum.

# Note
There is another solution which flip row first


# Solution
## Solution 1: in place replace 
Key difficulty = range of inner loop (otherwise, the ard processed cell will be process again) 
## S1
Convert problem to [Best time to buy and sell stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) with prefix sum

```java
public int maxSubArray(int[] nums) {
        if (nums.length == 1) return nums[0];
        int[] pref = new int[nums.length+1];
        // prefix sum. need to consider 0 element
        for (int i =1; i <=nums.length; i++){
            pref[i] = pref[i-1] + nums[i-1];
        }

        int maxSum = Integer.MIN_VALUE; 
        int min = pref[0];
        // similar to jump game - iterate through while updating min
        for (int i =1; i <=nums.length; i++){
            maxSum = Math.max(maxSum, pref[i] - min);
            if (pref[i]< min) min = pref[i];
        }

        return maxSum;
    }
```

## S2 (optimized)
```java 
    // for every number, either we take it as tail of the sequence, or as the begining of the sequence
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0], maxEndHere = nums[0];
        for (int i =1; i<nums.length; i++){
            maxEndHere = Math.max(maxEndHere + nums[i], nums[i]);
            maxSoFar = Math.max(maxEndHere, maxSoFar);
        }
        return maxSoFar;
    } 
```