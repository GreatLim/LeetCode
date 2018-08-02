# 222. Count Complete Tree Nodes

## Description

Given a **complete** binary tree, count the number of nodes.

**Note:**

**Definition of a complete binary tree from Wikipedia:**
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

**Example:**

```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```

##  Solution

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
    public int countNodes(TreeNode root) {
        if(root == null) return 0;
        int h = height(root);
        if(h - height(root.right) == 1) return (1 << (h - 1)) + countNodes(root.right);
        else return (1 << (h - 2)) + + countNodes(root.left);
    }
    
    public int height(TreeNode root) {
        if(root == null) return 0;
        return height(root.left) + 1;
    }
    
}
```

