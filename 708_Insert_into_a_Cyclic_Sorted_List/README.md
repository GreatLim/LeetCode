# 708. Insert into a Cyclic Sorted List

## Description

------

Given a node from a cyclic linked list which is sorted in ascending order, write a function to insert a value into the list such that it remains a cyclic sorted list. The given node can be a reference to *any* single node in the list, and may not be necessarily the smallest value in the cyclic list.

If there are multiple suitable places for insertion, you may choose any place to insert the new value. After the insertion, the cyclic list should remain sorted.

If the list is empty (i.e., given node is `null`), you should create a new single cyclic list and return the reference to that single node. Otherwise, you should return the original given node.

The following example may help you understand the problem better:

 

![img](https://leetcode.com/static/images/problemset/InsertCyclicBefore.png)
In the figure above, there is a cyclic sorted list of three elements. You are given a reference to the node with value 3, and we need to insert 2 into the list.

 

 

 

![img](https://leetcode.com/static/images/problemset/InsertCyclicAfter.png)
The new node should insert between node 1 and node 3. After the insertion, the list should look like this, and we should still return node 3.



## Solution

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;

    public Node() {}

    public Node(int _val,Node _next) {
        val = _val;
        next = _next;
    }
};
*/
class Solution {
    public Node insert(Node head, int insertVal) {
        if (head == null) {
            head = new Node();
            head.val = insertVal;
            head.next = head;
            return head;
        }
        Node cur = head.next, pre = head;
        while(cur != head) {
            if(cur.val < pre.val) break;
            pre = cur;
            cur = cur.next;
        }
        
        
        Node sentinel = new Node(0, cur), tail = pre;
        pre.next = null;
        pre = sentinel;
        
        while (cur != null && insertVal > cur.val) {
            pre = cur;
            cur = cur.next;
        }
        pre.next = new Node(insertVal, cur);
        if(cur == null) tail = pre.next;
        tail.next = sentinel.next;
        return head;
    }
}
```

