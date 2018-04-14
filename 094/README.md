# 94. Binary Tree Inorder Traversal

## Description
Given a binary tree, return the *inorder* traversal of its nodes' values.

For example:
Given binary tree `[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return `[1,3,2]`.

**Note:** Recursive solution is trivial, could you do it iteratively?

## Solution

### Iterative Solution

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new LinkedList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode cur = root;
        while(!stack.isEmpty() || cur != null) {
            while(cur!= null) {
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            result.add(cur.val);
            cur = cur.right;
        }
        return result;
    }
}
```

### Recursive solution

```java
class Solution {
    List<Integer> result = new LinkedList<Integer>();
    public List<Integer> inorderTraversal(TreeNode root) {
        if(root == null) return result;
        if(root.left != null) {
            inorderTraversal(root.left);
        }
        result.add(root.val);
        if(root.right != null) {
            inorderTraversal(root.right);
        }        
        return result;
    }
}
```

