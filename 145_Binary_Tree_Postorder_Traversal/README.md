# 145. Binary Tree Postorder Traversal

##  Description

Given a binary tree, return the *postorder* traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

 

## Solution

### Recursive Solution

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
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        helper(root, list);
        return list;
    }
    
    public void helper(TreeNode root, LinkedList<Integer> list) {
        if(root == null) return;
        helper(root.left, list);
        helper(root.right, list);
        list.add(root.val);
    }
}
```

