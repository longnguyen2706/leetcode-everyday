# Description
[Gas station](https://leetcode.com/problems/gas-station/description/)

There are n gas stations along a circular route, where the amount of gas at the ith station is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from the ith station to its next (i + 1)th station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique

# Note
Key points:
- Calculte the gas left at each station by gas[i] - cost[i]
- Let's start from any station. Let's calculate cumm_gas starting from that station onward. If we can reach the next station (cumm_gas>=0), we continue. Otherwise, we start from the next valid station. 
- Key point here is since we check cumm_gas>=0 every step, from (start_idx -> invalid_index), we could not find any valid index in such range. Let's say we find one valid idx and start from there, it wont be good, since removing (start_idx -> idx) region will only make the cumm_gas smaller (and it's already less than 0)

# Solution
## Solution 1
```python
 def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        cumm_gas, cumm_gas_total = 0, 0
        ans = 0
        for i in range(len(gas)):
            cumm_gas+= gas[i]-cost[i]
            cumm_gas_total+= gas[i]-cost[i]
            if cumm_gas<0:
                cumm_gas = 0
                ans = i+1
        return ans if cumm_gas_total>=0 else -1
```