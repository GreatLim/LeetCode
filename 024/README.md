# 24. Swap Nodes in Pairs

## Description

Given a linked list, swap every two adjacent nodes and return its head.

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

**Note:**

- Your algorithm should use only constant extra space.
- You may **not** modify the values in the list's nodes, only nodes itself may be changed.

## Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode n0 = sentinel;
        ListNode n1 = n0.next;
        ListNode n2 = n1.next;
        while(n1 != null && n1.next != null) {
            n1.next = n2.next;
            n0.next = n2;
            n2.next = n1;
            n0 = n1;
            n1 = n1.next;
            if(n1 != null) n2 = n1.next;
        }
        return sentinel.next;
    }
}
```

### 

