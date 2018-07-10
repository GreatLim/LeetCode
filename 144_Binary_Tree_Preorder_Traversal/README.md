# 144. Binary Tree Preorder Traversal

## Description 

Given a binary tree, return the *preorder* traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?



## Solution

### Iterative Version

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
    public List<Integer> preorderTraversal(TreeNode root) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        stack.push(node);
        
        while(!stack.isEmpty()){
            node = stack.pop();
            while(node != null) {
                list.add(node.val);
                stack.push(node.right);
                node = node.left;
            }
        }
        
        return list;
    }
}
```



### Recursive Version

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
    public List<Integer> preorderTraversal(TreeNode root) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        helper(root, list);
        return list;
    }
    
    public void helper(TreeNode root, LinkedList<Integer> list) {
        if(root == null) return;
        list.add(root.val);
        helper(root.left, list);
        helper(root.right, list);
    }
}
```

