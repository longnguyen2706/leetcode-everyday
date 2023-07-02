# Description
[Task Scheduler](https://leetcode.com/problems/task-scheduler/description/)

Given a characters array tasks, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.

However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks.

Return the least number of units of times that the CPU will take to finish all the given tasks.

# Note
It is a very non-straightfoward problem.

Key points: 
- Find number of CPU idles. The result equals to number of CPU idles + number of tasks.
- Need to sort the tasks by frequency. Max freq first -> create some idle time slot. We then fill the idle time slot with other tasks.
- Let's consider this case: 
    ```python
    A _ A _ A, n =1 
    We have B and C with same freq as A.
    
    A _ A _ A  -> A B A B A B -> A B C A B C A B C (no slot left we can still insert C, since it does not violate the rule)
    ```
We could even find a math formula for this problem.
- Let f_max is max_freq and n_max is number of tasks with max_freq.
- See https://leetcode.com/problems/task-scheduler/editorial/ for more details.

# Solution
## Solution 1
Greedy

```python
class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        freq = [0] * 26
        for t in tasks: 
            idx = ord(t) - ord ('A')
            freq[idx] +=1; 

        freq.sort()

        f_max = freq.pop()
        idle_time = (f_max-1)*n # n-1 slit 

        while freq and idle_time>0:
            idle_time-=min(freq.pop(), f_max-1)
        idle_time=max(0, idle_time)

        return idle_time+len(tasks)

```