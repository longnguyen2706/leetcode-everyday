# Description
[Merge Two Sorted List] (https://leetcode.com/problems/merge-two-sorted-lists/description/)
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

# Note
- Time taken: < 5 mins

# Solution 
## 1st Solution
```python
class Solution:
    def mergeTwoLists(self, h1: Optional[ListNode], h2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        cur = dummy
        while h1 and h2: 
            if h1.val<h2.val:
                cur.next = h1
                h1 = h1.next
            else: 
                cur.next = h2
                h2 = h2.next
            cur = cur.next
        while h1: 
            cur.next = h1
            h1 = h1.next
            cur = cur.next
        while h2: 
            cur.next = h2
            h2 = h2.next
            cur = cur.next
        return dummy.next
```

## 2nd Solution
Better
```python
class Solution:
    def mergeTwoLists(self, h1: Optional[ListNode], h2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        cur = dummy
        while h1 and h2: 
            if h1.val<h2.val:
                cur.next = h1
                h1 = h1.next
            else: 
                cur.next = h2
                h2 = h2.next
            cur = cur.next
        
        cur.next =  h1 if h1 else h2
        
        return dummy.next
```

## 3rd Solution
Recursive 
```python
class Solution: 
    def mergeTwoLists(self, h1: Optional[ListNode], h2: Optional[ListNode]) -> Optional[ListNode]:
        if h1 is None:
            return h2
        if h2 is None:
            return h1
        if h1.val< h2.val: 
            h1.next = self.mergeTwoLists(h1.next, h2)
            return h1
        else: 
            h2.next = self.mergeTwoLists(h1, h2.next)
            return h2
```