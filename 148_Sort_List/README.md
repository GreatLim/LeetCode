# 148. Sort List

##  Description

Sort a linked list in *O*(*n* log *n*) time using constant space complexity.

**Example 1:**

```
Input: 4->2->1->3
Output: 1->2->3->4
```

**Example 2:**

```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
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
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode slow = head;
        ListNode fast = head;
        ListNode pre = null;
        
        while(fast != null && fast.next != null) {
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        } 
        pre.next = null;
        
        head = sortList(head);
        slow = sortList(slow);
        return merge(head, slow);
    }
    
    private ListNode merge(ListNode n1, ListNode n2) {
        if(n1 == null) return n2;
        if(n2 == null) return n1;
        
        ListNode sentinel = new ListNode(0);
        ListNode n = sentinel;
        while(n1 != null && n2 != null) {
            if(n1.val < n2.val) {
                n.next = n1;
                n = n1;
                n1 = n1.next;
            } else {
                n.next = n2;
                n = n2;
                n2 = n2.next;
            }
        }
        
        if(n1 != null) n.next = n1;
        if(n2 != null) n.next = n2;
        
        return sentinel.next;
    }
}
```





