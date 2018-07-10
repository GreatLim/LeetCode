# 160. Intersection of Two Linked Lists

## Description

Write a program to find the node at which the intersection of two singly linked lists begins.

 

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.

 

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

**Credits:**
Special thanks to [@stellari](https://oj.leetcode.com/discuss/user/stellari) for adding this problem and creating all test cases.

## Crack

* 将A和B看成两个环，则肯定会在某个时刻相遇于c1

## Solution

### Concise Version

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null) return null;
        ListNode n1 = headA;
        ListNode n2 = headB;
        while(n1 != n2) {
            n1 = (n1 == null) ? headA : n1.next;
            n2 = (n2 == null) ? headB : n2.next;
        }
        return n1;
    }
}
```



### Fisrt try

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode n1 = headA;
        ListNode n2 = headB;
        if(n1 == null || n2 == null) return null;
        while(n1.next != null && n2.next != null) {
            if(n1 == n2) return n1;
            n1 = n1.next;
            n2 = n2.next;
        }
        System.out.println(n1.val);
        System.out.println(n2.val);
        if(n1.next == null) {
            ListNode temp = n2;
            n1 = headA;
            n2 = headB;
            while(temp.next != null) {
                temp = temp.next;
                n2 = n2.next;
                if(n2 == null) return null;
            }
        } else {
            ListNode temp = n1;
            n1 = headA;
            n2 = headB;
            while(temp.next != null) {
                temp = temp.next;
                n1 = n1.next;
                if(n1 == null) return null;
            }
        }
        System.out.println(n1.val);
        System.out.println(n2.val);
        while(n1 != null && n2 != null) {
            if(n1 == n2) return n1;
            n1 = n1.next;
            n2 = n2.next; 
        }
        return null;
    }
}
```

