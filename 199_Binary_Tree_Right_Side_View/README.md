# 199. Binary Tree Right Side View

## Description

Given a binary tree, imagine yourself standing on the *right* side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

## Solution

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        dfs(root, 0, res);
        return res;
    }
    
    public void dfs(TreeNode root, int depth, List<Integer> list) {
        if(root == null) return;
        if(depth >= list.size()) list.add(root.val);
        dfs(root.right, depth + 1, list);
        dfs(root.left, depth + 1, list);
    }
}
```



### BFS

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
    public List<Integer> rightSideView(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        LinkedList<Integer> res = new LinkedList<Integer>();
        if(root == null) return res;
        q.add(root);
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i = 0; i < size; i++) {
                TreeNode n = q.poll();
                if(n.left != null) q.offer(n.left);
                if(n.right != null) q.offer(n.right);
                if(i == size - 1) res.add(n.val);
            }
        }
        return res;
    }
}
```

