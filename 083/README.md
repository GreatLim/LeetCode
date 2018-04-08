# 83. Remove Duplicates from Sorted List
## Description
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.
## Solution
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        //ListNode sentinel = new ListNode(0);
        //sentinel.next = head;
        ListNode fast = head;
        while(fast != null) {
            while (fast.next != null && fast.next.val == fast.val) {
                fast.next = fast.next.next;
            }
            fast = fast.next;
        }
        return head;
    }
}
```

