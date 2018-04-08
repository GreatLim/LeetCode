# 82. Remove Duplicates from Sorted List II
## Description
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.

## Solution
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null) return null;
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode fast = head;
        ListNode slow = sentinel;
        int mark = 0;
        while(fast != null) {
            while(fast.next != null && fast.next.val == fast.val) {
                fast = fast.next;
                mark = 1;
            }
            if(mark == 1) {
                slow.next = fast.next;
                mark = 0;
            } else {
                slow = slow.next;
            }
            fast = fast.next;
        }
        return sentinel.next;
    }
}
```


