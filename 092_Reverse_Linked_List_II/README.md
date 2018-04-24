# 92. Reverse Linked List II

## Description
Reverse a linked list from position *m* to *n*. Do it in one-pass.

**Note:** 1 ≤ *m* ≤ *n* ≤ length of list.

**Example:**

```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode slow = sentinel;
        ListNode fast;
        for(int i = 0; i < m - 1; i++) {
            slow = slow.next;
        }
        fast = slow.next;
        for(int i = 0; i < n - m; i++) {
            ListNode temp = fast.next;
            fast.next = temp.next;
            temp.next = slow.next;
            slow.next = temp;
        }
        return sentinel.next;
    }
}
```

