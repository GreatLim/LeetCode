# 530. Minimum Absolute Difference in BST

## Description

Given a binary search tree with non-negative values, find the minimum [absolute difference](https://en.wikipedia.org/wiki/Absolute_difference) between values of any two nodes.

**Example:**

```
Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```

**Note:** There are at least two nodes in this BST.

## Solution

### Concise Version

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
    int min = Integer.MAX_VALUE;
    TreeNode prev;
    
    public int getMinimumDifference(TreeNode root) {
        if(root == null) return Integer.MAX_VALUE;
        getMinimumDifference(root.left);
        if(prev != null) min = Math.min(min, root.val - prev.val);
        prev = root;
        getMinimumDifference(root.right);
        return min;
    }
}
```

### Fisrt try

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
    public int getMinimumDifference(TreeNode root) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        inorder(root, list);
        int min = Integer.MAX_VALUE;
        for(int i = 1; i < list.size(); i++) {
            min = Math.min(list.get(i) - list.get(i - 1), min);
        }
        return min;
    }
    
    public void inorder(TreeNode node, LinkedList<Integer> list) {
        if(node == null) return;
        
        inorder(node.left, list);
        list.add(node.val);
        inorder(node.right,list);
    }
}
```

## Notes

* you can define some instance variables to record somthing like `prev`