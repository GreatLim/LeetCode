# 113. Path Sum II

## Description

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**

Given the below binary tree and `sum = 22`,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```

Return:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

## Soution

### dis & backtrack

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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        List<Integer> tempList = new LinkedList<Integer>();
        backtrack(root, sum, res, tempList);
        return res;
    }
    
    public void backtrack(TreeNode root, int target, List<List<Integer>> list, List<Integer> tempList) {
        if(root == null) return;
        target = target - root.val;
        tempList.add(root.val);
        if(root.left == null && root.right == null && target == 0) 
            list.add(new LinkedList(tempList));
        backtrack(root.left, target, list, tempList);
        backtrack(root.right, target, list, tempList);
        tempList.remove(tempList.size() - 1);
    }
}
```

