# 110. Balanced Binary Tree

##  Description

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

**Example 1:**

Given the following tree `[3,9,20,null,null,15,7]`:

```
    3
   / \
  9  20
    /  \
   15   7
```

Return true.
**Example 2:**

Given the following tree `[1,2,2,3,3,null,null,4,4]`:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

Return false.

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
    HashMap<TreeNode, Integer> map = new HashMap<TreeNode, Integer>();
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        int left = depth(root.left);
        int right = depth(root.right);
        if(Math.abs(left - right) <= 1 && isBalanced(root.left) && isBalanced(root.right)) return true;
        return false;
    }
    
    public int depth (TreeNode root) {
        if(root == null) return 0;
        // if(map.containsKey(root)) return map.get(root);
        int max = Math.max(depth(root.left), depth(root.right)) + 1;
        // map.put(root, max);
        return max;
    }  
} 
```

