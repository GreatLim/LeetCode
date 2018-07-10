# 143. Reorder List

## Description

Given a singly linked list *L*: *L*0→*L*1→…→*Ln*-1→*Ln*,
reorder it to: *L*0→*Ln*→*L*1→*Ln*-1→*L*2→*Ln*-2→…

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

**Example 1:**

```
Given 1->2->3->4, reorder it to 1->4->2->3.
```

**Example 2:**

```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```

##  Solution

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
    public void reorderList(ListNode head) {
        if(head == null) return;
        ListNode sentinel = new ListNode(0);
        ListNode fast = head;
        ListNode slow = head;
        ListNode temp;
        
        while(fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        
        temp = slow.next;
        slow.next = null;

        slow = temp;
        
        while(slow != null) {
            temp = slow.next;
            slow.next = sentinel.next;
            sentinel.next = slow;
            slow = temp;
        }
        
        slow = head;
        fast = head.next;
        
        while(sentinel.next != null) {
            temp = sentinel.next;
            sentinel.next = sentinel.next.next;
            slow.next = temp;
            temp.next = fast;
            slow = fast;
            if(slow != null) fast = slow.next;
        }
        
    }
}
```

