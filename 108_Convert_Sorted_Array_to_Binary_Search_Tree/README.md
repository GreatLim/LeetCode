# 108. Convert Sorted Array to Binary Search Tree

## Description

```
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

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
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(0, nums.length - 1, nums);
    }
    
    public TreeNode helper(int lo, int hi, int[] nums) {
        if(hi < lo) return null;
        int mid = (lo + hi) / 2;
        TreeNode n = new TreeNode(nums[mid]);
        n.left = helper(lo, mid - 1, nums);
        n.right = helper(mid + 1, hi, nums);
        return n;
    }
}
```

