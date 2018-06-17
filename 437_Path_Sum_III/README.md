# 437. Path Sum III

## Description

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

## Crack

这道题首先想到dfs

采用递归要分为两个部分，一个是pathSum，一个是dfs

dfs的递归只考虑包括root的path

而pathSum则还需要root.left和root.right的所有path（无论是否包括root）

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
    public int pathSum(TreeNode root, int sum) {
        if(root == null) return 0;
        return dfs(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
    }
    
    public int dfs(TreeNode root, int target) {
        if(root == null) return 0;
        target = target - root.val;
        return (target == 0 ? 1 : 0) + dfs(root.left, target) + dfs(root.right, target);
    }
}
```

