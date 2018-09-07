# 285. Inorder Successor in BST

## Description

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

**Note**: If the given node has no in-order successor in the tree, return `null`.

**Example 1:**

```
Input: root = [2,1,3], p = 1

  2
 / \
1   3

Output: 2
```

**Example 2:**

```
Input: root = [5,3,6,2,4,null,null,1], p = 6

      5
     / \
    3   6
   / \
  2   4
 /   
1

Output: null
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
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root == null) return null;
        if(p.val >= root.val) return inorderSuccessor(root.right, p);
        else {
            TreeNode temp = inorderSuccessor(root.left, p);
            if(temp == null) return root;
            else return temp;
        }
    }
}
```

