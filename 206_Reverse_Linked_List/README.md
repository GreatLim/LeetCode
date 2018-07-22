# 206. Reverse Linked List

## Description

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?

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
    public ListNode reverseList(ListNode head) {
        ListNode sentinel = new ListNode(0);
        ListNode cur = head;
        while(cur != null) {
            ListNode temp = sentinel.next;
            sentinel.next = cur;
            cur = cur.next;
            sentinel.next.next = temp;
        }
        return sentinel.next;
    }
}
```

 