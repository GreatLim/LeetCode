# 572. Subtree of Another Tree

## Description

Given two non-empty binary trees **s** and **t**, check whether tree **t** has exactly the same structure and node values with a subtree of **s**. A subtree of **s** is a tree consists of a node in **s** and all of this node's descendants. The tree **s** could also be considered as a subtree of itself.

**Example 1:**
Given tree s:

```
     3
    / \
   4   5
  / \
 1   2
```

```
   4 
  / \
 1   2
```

 

true

**Example 2:**
Given tree s:

```
     3
    / \
   4   5
  / \
 1   2
    /
   0
```

```
   4
  / \
 1   2
```

 

false



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
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (t == null || isTheSame(s, t)) return true;
        if (s == null) return false;
        return isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    
    public boolean isTheSame(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        if ((s == null || t == null)) return false;
        if (s.val == t.val && isTheSame(s.left, t.left) && isTheSame(s.right, t.right)) return true;
        return false;
    }
}
```

 