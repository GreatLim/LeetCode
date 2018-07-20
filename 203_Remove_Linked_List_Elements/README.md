# 203. Remove Linked List Elements

##  Description

Remove all elements from a linked list of integers that have value **val**.

**Example:**

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
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
    public ListNode removeElements(ListNode head, int val) {
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode pre = sentinel;
        ListNode cur = head;
        while(cur != null) {
            if(cur.val == val) pre.next = cur.next;
            else pre = cur;
            cur = cur.next;
        }
        return sentinel.next;
    }
}
```

