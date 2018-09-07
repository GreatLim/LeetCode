# 146. LRU Cache

## Description

Design and implement a data structure for [Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Follow up:**
Could you do both operations in **O(1)** time complexity?

**Example:**

```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```



## Solution

```java
class LRUCache {
    private DListNode sentinel = new DListNode(0, 0);
    private HashMap<Integer, DListNode> cache = new HashMap<>();
    private int capacity;

    public LRUCache(int capacity) {
        sentinel.next = sentinel;
        sentinel.pre = sentinel;
        this.capacity = capacity;
    }
    
    public int get(int key) {
        if(!cache.containsKey(key)) return -1;
        DListNode n = cache.get(key);
        moveToHead(n);
        return n.val;
    }
    
    public void put(int key, int value) {
        if(!cache.containsKey(key)) {
            if(cache.size() == capacity) {
                cache.remove(sentinel.pre.key);
                removeTail();
            }
            DListNode n = new DListNode(key, value);
            addToHead(n);
            cache.put(key, n);
        } else {
            DListNode n = cache.get(key);
            n.val = value;
            moveToHead(n);
        }
    }
    
    private void remove(DListNode n) {
        DListNode pre = n.pre;
        DListNode next = n.next;
        pre.next = next;
        next.pre = pre;
    }
    
    private void moveToHead(DListNode n) {
        if(n == sentinel.next) return;
        remove(n);
        addToHead(n);
    }
    
    private void addToHead(DListNode n) {
        DListNode next = sentinel.next;
        sentinel.next = n;
        n.pre = sentinel;
        n.next = next;
        next.pre = n;
    }
    
    private void removeTail() {
        remove(sentinel.pre);
    }
    
    
    private class DListNode {
        private DListNode pre;
        private DListNode next;
        private int val;
        private int key;
        private DListNode(int key, int val) {
            this.val = val;
            this.key = key;
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

