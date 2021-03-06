# 102. Binary Tree Level Order Traversal

## Description

Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

##Solutions

### DFS

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        dfs(root, 0, res);
        return res;
    }
    
    public void dfs(TreeNode root, int depth, List<List<Integer>> res) {
        if(root == null) return;
        if(depth == res.size()) res.add(new LinkedList<Integer>());
        res.get(depth).add(root.val);
        dfs(root.left, depth + 1, res);
        dfs(root.right, depth + 1, res);
    }
}
```

### Concise Version (BFS)

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        if(root == null) return res;     
        q.offer(root);
        while(!q.isEmpty()) {
            int j = q.size();
            List<Integer> temp = new LinkedList<Integer>();
            for(int i = 0; i < j; i++) {
                TreeNode n = q.poll();
                if(n.left != null) q.offer(n.left);
                if(n.right != null) q.offer(n.right);
                temp.add(n.val);
            }
            res.add(temp);
        }
        return res;
    }
}
```



### First try (BFS)

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<List<TreeNode>> q = new LinkedList<List<TreeNode>>();
        List<TreeNode> cur = new LinkedList<TreeNode>();
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        if(root == null) return res;
        cur.add(root);
        q.offer(cur);
        while(!cur.isEmpty()) {
            List<Integer> temp = new LinkedList<Integer>();
            List<TreeNode> next = new LinkedList<TreeNode>();
            for(TreeNode n : cur) {
                temp.add(n.val);
                if(n.left != null) next.add(n.left);
                if(n.right != null) next.add(n.right);
            }
            res.add(temp);
            cur = next;
        }
        return res;
    }
}
```

