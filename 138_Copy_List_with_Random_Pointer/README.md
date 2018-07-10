## 138. Copy List with Random Pointer

##  Description

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

## Solution

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null) return null;
        HashMap<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
        RandomListNode first = head;
        RandomListNode pre = null;
        while(head != null) {
            map.put(head, map.getOrDefault(head, new RandomListNode(head.label)));
            if(pre != null) pre.next = map.get(head);
            if(head.random != null) {
                map.put(head.random, map.getOrDefault(head.random, new RandomListNode(head.random.label)));
                map.get(head).random = map.get(head.random);
            }
            pre = map.get(head);
            head = head.next;
        }
        return map.get(first);
    }
}
```

