# 23. Merge k Sorted Lists

## Description

Merge *k* sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Example:**

```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## Soluiton

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
    public ListNode mergeKLists(ListNode[] lists) {
        int size = lists.length;
        if(size == 0) return null;
        PriorityQueue<ListNode> queue = new PriorityQueue<ListNode>(size, new Comparator<ListNode>() {
            public int compare(ListNode n1, ListNode n2) {
                return Integer.compare(n1.val, n2.val);
            }
        });
        for (ListNode list : lists) {
            if(list != null) queue.add(list);
        }
        ListNode sentinel = new ListNode(0);
        ListNode tail = sentinel;
        while(!queue.isEmpty()) {
            tail.next = queue.poll();
            tail = tail.next;
            if(tail.next != null)
                queue.add(tail.next);
        }
        return sentinel.next;
    }
}
```

## Complexity Analysis

- **Complexity Analysis**
  - Time complexity : O(Nlogk) where k is the number of linked lists.
    - The comparison cost will be reduced to O(logk) for every pop and insertion to priority queue. But finding the node with the smallest value just costs O(1) time.
    - There are N nodes in the final linked list.
  - Space complexity :
    - O(n) Creating a new linked list costs O(n) space.
    - O(k) The code above present applies in-place method which cost O(1) space. And the priority queue (often implemented with heaps) costs O(k) space (it's far less than NN in most situations).