# Description
[Meeting Room](https://leetcode.com/problems/meeting-rooms/description/)

Given an array of meeting time intervals where intervals[i] = [starti, endi], determine if a person could attend all meetings.
# Note

# Solution 
## Solution 1
```python 
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        # the person can attend all meeting if there is no overlapping between interval 
        # sort by start
        if len(intervals) < 2: 
            return True 

        intervals.sort(key = lambda x: x[0])
        end = intervals[0][1]
        for i in range (1, len(intervals)):
            if intervals[i][0]<end: 
                return False
            end = intervals[i][1]

        return True
```

## Better solution
```python 
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
       intervals.sort(key = lambda x: x.start)
       for i in range (1, len(intervals)):
           if intervals[i].start < intervals[i-1].end:
               return False
        return True
```
