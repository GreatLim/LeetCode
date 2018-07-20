# 865. Smallest Subtree with all the Deepest Nodes

## Description

Given a binary tree rooted at `root`, the *depth* of each node is the shortest distance to the root.

A node is *deepest* if it has the largest depth possible among any node in the entire tree.

The subtree of a node is that node, plus the set of all descendants of that node.

Return the node with the largest depth such that it contains all the deepest nodes in its subtree.

 

**Example 1:**

```
Input: [3,5,1,6,2,0,8,null,null,7,4]
Output: [2,7,4]
Explanation:



We return the node with value 2, colored in yellow in the diagram.
The nodes colored in blue are the deepest nodes of the tree.
The input "[3, 5, 1, 6, 2, 0, 8, null, null, 7, 4]" is a serialization of the given tree.
The output "[2, 7, 4]" is a serialization of the subtree rooted at the node with value 2.
Both the input and output have TreeNode type.
```

 

**Note:**

- The number of nodes in the tree will be between 1 and 500.
- The values of each node are unique.

## Crack

*  `map` 记录了`TreeNode` 和对应能到达叶子最大距离
* 当某个 `root` 的 `left` 和 `right` 相同时，那么 `root` 就是目标的 `TreeNode`

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
    public TreeNode subtreeWithAllDeepest(TreeNode root) {
        HashMap<TreeNode, Integer> map = new HashMap<TreeNode, Integer>();
        return dfs(root, map);
    }
    
    public int depth(TreeNode root, HashMap<TreeNode, Integer> map) {
        if(root == null) return 0;
        if(map.containsKey(root)) return map.get(root);
        int max = Math.max(depth(root.left, map) + 1, depth(root.right, map) + 1);
        map.put(root, max);
        return max;
    }
    
    public TreeNode dfs(TreeNode root, HashMap<TreeNode, Integer> map) {
        int left = depth(root.left, map);
        int right = depth(root.right, map);
        if(left == right) return root;
        if(left < right) return dfs(root.right, map);
        return dfs(root.left, map);
    }
}
```

