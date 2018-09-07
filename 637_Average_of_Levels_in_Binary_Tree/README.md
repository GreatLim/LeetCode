# 637. Average of Levels in Binary Tree

## Description

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

**Example 1:**

```
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

**Note:**

1. The range of node's value is in the range of 32-bit signed integer.

## Solution

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        LinkedList<Double> res = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            long size = q.size(), sum = 0;
            for (int i = 0; i < size; i++) {
                TreeNode n = q.poll();
                sum += n.val;
                if(n.left != null) q.offer(n.left);
                if(n.right != null) q.offer(n.right);
            }
            res.add((double) sum / size);
        }
        return res;
    }
}
```

