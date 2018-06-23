# 124. Binary Tree Maximum Path Sum

## Description

Given a **non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

**Example 2:**

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

## Solution

### First Try

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
    int max = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        helper(root);
        return max;
    }
    
    public void helper(TreeNode root) {
        if(root == null) return;
        helper(root.left);
        helper(root.right);
        int sum = root.val;
        if(root.left != null && root.left.val > 0) sum += root.left.val;
        if(root.right != null && root.right.val > 0) sum += root.right.val;
        if(root.left != null && root.left.val > 0 && root.right != null && root.right.val > 0)
            root.val += Math.max(root.left.val, root.right.val);
        else if(root.left != null && root.left.val > 0) root.val += root.left.val;
        else if(root.right != null && root.right.val > 0) root.val += root.right.val;
        max = Math.max(max, sum);
    }
}
```

