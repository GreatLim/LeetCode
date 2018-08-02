# 257. Binary Tree Paths

## Description

Given a binary tree, return all root-to-leaf paths.

**Note:** A leaf is a node with no children.

**Example:**

```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

## Solution

### Backtrack & DFS

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new LinkedList();
        backtrack(res, new StringBuilder(), root);
        return res;
    }
    
    public void backtrack(List<String> res, StringBuilder sb, TreeNode root) {
        if(root == null) return;
        int len = sb.length();
        sb.append(root.val);
        if(root.left == null && root.right == null) {
            res.add(new String(sb));
        }
        else {
            sb.append("->");
            backtrack(res, sb, root.left);
            backtrack(res, sb, root.right);
        }
        sb.setLength(len);
        
    }
}
```

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new LinkedList();
        backtrack(res, new StringBuilder(), root);
        return res;
    }
    
    public void backtrack(List<String> res, StringBuilder sb, TreeNode root) {
        if(root == null) return;
        if(root.left == null && root.right == null) {
            sb.append(root.val);
            res.add(new String(sb));
        } else {
            sb.append(root.val).append("->");
            int len = sb.length();
            backtrack(res, sb, root.left);
            sb.setLength(len);
            backtrack(res, sb, root.right);
            sb.setLength(len);
        }
    }
}
```

