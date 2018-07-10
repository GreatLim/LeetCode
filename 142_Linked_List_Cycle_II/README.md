# 142. Linked List Cycle II

##  Description

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

**Note:** Do not modify the linked list.

**Follow up**:
Can you solve it without using extra space?

## Solution

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        boolean isCycle = false;
        ListNode fast = head;
        ListNode slow = head;
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow) {
                isCycle = true;
                break;
            }
        }
        if(!isCycle) return null;
        fast = head;
        while(fast != slow) {
            fast = fast.next;
            slow = slow.next;
        }
        return fast;
    }
}
```

## Note

```
    我们可以使用两枚指针oneStep、twoStep，每次分别移动1、2步，若存在圈，则两枚指针在第1、2、3、4...n圈后终会相遇(我们并不知道会在第几圈相遇)
    整个圈：1 -> 2 -> 3 -> 1
    部分圈：1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 11 -> 12 -> 13 -> 14 -> 15 -> 5(跟5相连，形成圈)
           |<--------s------->| |<----------------------------r------------------------>|
           |<--------------------k----------------------->|
           |<------------------------------------2k--------------------------------------  
                                 ------------------------>|
           我们假设链表头到圈始点长度为s，圈长度为r，移动两枚指针后，相遇时oneStep走了k步，twoStep则走了2k步：
           1. 我们知道相遇时twoStep比oneStep多走了n圈，(1)(2k - s) - (k - s) = nr  =>  k = nr  =>  k = r (n = 1)
              (注意：我们取n = 1，即twoStep比oneStep多走一圈，因为一旦相遇我们便知道了有圈)

            k = r 于是便有了下面这幅图：
    部分圈：1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 11 -> 12 -> 13 -> 14 -> 15 -> 5(跟5相连，形成圈)
           |<--------s------->| |<----------------------------r------------------------>|        
           |<--------------------r----------------------->|
           |<------------------------------------2r--------------------------------------  
                                 ------------------------>|
           2. s(我们知道s就是我们要求的圈始点)怎么求呢？
       
           3. 眼尖的同学可能已经看出来了，没错 s + r = 链表总长度，我们再将oneStep或者twoStep移动s就会再次相遇！
           
           于是便有了下面这幅图：
    部分圈：1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 11 -> 12 -> 13 -> 14 -> 15 -> 5(跟5相连，形成圈)
           |<--------s------->| |<----------------------------r------------------------>|        
           |<--------------------r----------------------->| |************* s ************|
           |<------------------------------------2r--------------------------------------  
                                 ------------------------>| |************* s ************|
          
          4. 现在我们让oneStep再次从head开始，oneStep和twoStep每次均移动一步，再次相遇就会在起始点咯！

          5. 大家可以自行思考整个圈的情况是否如此.
```
