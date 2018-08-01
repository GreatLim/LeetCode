# 250. Count Univalue Subtrees

## Description

Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

**Example :**

```
Input:  root = [5,1,5,5,5,null,5]

              5
             / \
            1   5
           / \   \
          5   5   5

Output: 4
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
    private int count = 0;
    public int countUnivalSubtrees(TreeNode root) {
        isUnival(root);
        return count;
    }
    
    private boolean isUnival(TreeNode root) {
        if(root == null) return true;
        boolean left = isUnival(root.left), right = isUnival(root.right);
        if(left && right) {
            if(root.left != null && root.left.val != root.val) return false;
            if(root.right != null && root.right.val != root.val) return false;
            count++;
            return true;
        }
        return false;
    }
}
```

