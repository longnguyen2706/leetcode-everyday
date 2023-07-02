
# Description
[Hand of Straights](https://leetcode.com/problems/task-scheduler/description/)

Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size groupSize, and consists of groupSize consecutive cards.

Given an integer array hand where hand[i] is the value written on the ith card and an integer groupSize, return true if she can rearrange the cards, or false otherwise.

# Note
- Solution 1: it could be faster if we could use the deque, since we need to remove element from list

# Solution
## Solution 1

```python
class Solution:
    def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
        # check len(hand) divisible groupSize
        # sort, build freq map or map of val, index
        # for each number in sorted seq: find and update the map

        # 1 2 2 3 3 4 6 7 8 
        # map (val, freq). sort
        n = len(hand)
        if n % groupSize !=0: 
            return False

        m = {}
        for h in hand: 
            if h not in m: 
                m[h] = 1
            else:
                m[h] +=1 
        
        l = []
        for k in m.keys():
            l.append(k)
        l.sort()

        while n>0:
            val = l[0]
            for i in range (groupSize):
                if (i+val) not in m: 
                    return False
                m[i+val]-=1 
                if m[i+val] == 0: 
                    del m[i+val]
                    l.remove (i+val) # faster with deque
            n-=groupSize 
        return True        

```


