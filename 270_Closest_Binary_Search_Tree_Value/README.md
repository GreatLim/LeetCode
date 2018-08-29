# 270. Closest Binary Search Tree Value

## Description

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

- Given target value is a floating point.
- You are guaranteed to have only one unique value in the BST that is closest to the target.

**Example:**

```
Input: root = [4,2,5,1,3], target = 3.714286

    4
   / \
  2   5
 / \
1   3

Output: 4
```





## Soluiton

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
    TreeNode pre = null;
    
    public int closestValue(TreeNode root, double target) {
        if(root == null) return pre.val;
        pre = root;
        int parent = root.val;
        int kid = (target < root.val) ? closestValue(root.left, target) : closestValue(root.right, target);
        return Math.abs(parent - target) > Math.abs(kid - target) ? kid : parent;
    }
}
```

