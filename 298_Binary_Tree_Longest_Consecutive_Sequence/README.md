# 298. Binary Tree Longest Consecutive Sequence

## Description

Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

**Example 1:**

```
Input:

   1
    \
     3
    / \
   2   4
        \
         5

Output: 3

Explanation: Longest consecutive sequence path is 3-4-5, so return 3.
```

**Example 2:**

```
Input:

   2
    \
     3
    / 
   2    
  / 
 1

Output: 2 

Explanation: Longest consecutive sequence path is 2-3, not 3-2-1, so return 2.
```

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
    public int res = 0;
    
    public int longestConsecutive(TreeNode root) {
        helper(root);
        return res;
    }
    
    
    public int helper(TreeNode root) {
        if (root == null) return 0;
        int left = helper(root.left), right = helper(root.right), max = 1;
        if (root.left != null && root.val + 1 == root.left.val) max = left + 1;
        if (root.right != null && root.val + 1 == root.right.val) max = Math.max(max, right + 1);
        res = Math.max(res, max);
        return max;
    }
}
```

