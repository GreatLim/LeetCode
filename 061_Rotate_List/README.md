# 61. Rotate List
## Description
Given a list, rotate the list to the right by k places, where k is non-negative.


Example:

```
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```

## Solution
```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null) return null;
        ListNode fast = head;
        ListNode slow = head;
        int i = 1;
        while(fast.next!= null) {
            fast = fast.next;
            i++;
        }
        if(k % i == 0) return head;
        for(int j = 0; j < i - k % i - 1; j++) {
            slow = slow.next;
        }
        fast.next = head;
        head = slow.next;
        slow.next = null;
        return head;
    }
}
```

