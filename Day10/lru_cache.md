# Description
[LRU Cache](https://leetcode.com/problems/lru-cache/description/)

Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

# Note
- We need to use doubly linked list since we need to remove the node from tail (least recently used) and add node to head for any node that is queried by get or added by put
- To avoid duplicate value node inside the linked list, we need to use a dictionary to store the key and the node (instead of value) 
- We need to use dummy head and tail to avoid edge case when the linked list is empty

# Solution
## Solution 1
```python
class LRUCache:
    # get O(1): map (key, val)
    # remove LRU: linkedlist 
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.m = {}
        self.head = Node(-10, -10)
        self.tail = Node(-10, -10)
        self.head.next = self.tail
        self.tail.prev = self.head
     
    def get(self, key: int) -> int:
        if key not in self.m:
            return -1
        
        node = self.m[key]
        self.delete_node(node)
        self.add_to_head(node)
        
        return node.val
    
    def put(self, key: int, value: int) -> None:
        if key in self.m:
            self.delete_node(self.m[key]) # delete node, will add the node to head of the list later
        node = Node(key, value)
        self.m[key] = node
        # insert node to head 
        self.add_to_head(node)
            
        if len(self.m)> self.capacity: # delete the last node 
            node = self.tail.prev
            del self.m[node.key]
            self.delete_node(self.tail.prev)

      

    def delete_node(self, node):
        # delete node
        # head -> node1 ... -> node n -> tail
        if node != self.head: 
            node.prev.next = node.next
            node.next.prev = node.prev

    def add_to_head(self, node):
       # head -> node -> head.next
        next = self.head.next
        node.prev = self.head 
        node.next = next
        next.prev = node
        self.head.next = node 
        
    def print_ll(self, node):
        cur = node
        while cur: 
            print (cur.val,  end=' ')
            cur = cur.next
        print()

class Node:
    def __init__(self, key, val):
        self.prev = None
        self.next = None
        self.val = val
        self.key = key
    

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

## Solution 2 
Using build in libary 

```python
import collections

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.dic = collections.OrderedDict()

    def get(self, key: int) -> int:
        if key not in self.dic:
            return -1
        
        self.dic.move_to_end(key)
        return self.dic[key]
        
    def put(self, key: int, value: int) -> None:
        if key in self.dic:
            self.dic.move_to_end(key)
        
        self.dic[key] = value
        if len(self.dic) > self.capacity:
            self.dic.popitem(False)
```

```java
class LRUCache {
    int capacity;
    LinkedHashMap<Integer, Integer> dic;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        dic = new LinkedHashMap<>(5, 0.75f, true) {
            @Override
            protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
                return size() > capacity;
            }
        };
    }
    
    public int get(int key) {
        return dic.getOrDefault(key, -1);
    }
    
    public void put(int key, int value) {
        dic.put(key, value);
    }

}
```