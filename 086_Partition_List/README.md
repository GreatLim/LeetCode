# 86. Partition List

## Description
Given a linked list and a value *x*, partition it such that all nodes less than *x* come before nodes greater than or equal to *x*.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given `1->4->3->2->5->2` and *x* = 3,
return `1->2->2->4->3->5`.

## Solution

```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        if(head == null || head.next == null) return head;
        ListNode small = new ListNode(0), large = new ListNode(0);
        ListNode sentinel1 = small, sentinel2 = large;
        while(head != null) {
            if(head.val < x) {
                small.next = head;
                small = small.next;
            } else {
                large.next = head;
                large = large.next;
            }
            head = head.next;
        }
        large.next = null; // avoid cycle
        small.next = sentinel2.next;
        return sentinel1.next;
    }
}
```

This version is more concise than original one.

### Original solution

```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        if(head == null || head.next == null) return head;
        ListNode small = new ListNode(0), large = new ListNode(0);
        ListNode sentinel1 = small, sentinel2 = large;
        ListNode slow = head;
        ListNode fast = head.next;
        while(slow != null) {
            if(slow.val < x) {
                small.next = slow;
                small = small.next;
            } else {
                large.next = slow;
                large = large.next;
            }
            slow.next = null;
            slow = fast;
            fast = (fast != null) ? fast.next : null;
        }
        small.next = sentinel2.next;
        return sentinel1.next;
    }
}
```

