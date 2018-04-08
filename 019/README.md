# 19. Remove Nth Node From End of List
## Description
Given a linked list, remove the nth node from the end of list and return its head.

For example,

```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```

Note:
Given n will always be valid.
Try to do this in one pass.

##Solution
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode n1 = sentinel;
        ListNode n2 = sentinel;
        ListNode n3;
        for(int i = 0; i < n; i++) {
            n1 = n1.next;
        }
        while(n1.next != null) {
            n1 = n1.next;
            n2 = n2.next;
        }
        n3 = n2.next;
        n2.next = n3.next;
        n3.next = null;
        return sentinel.next;
    }
}
```


