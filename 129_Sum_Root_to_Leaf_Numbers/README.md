# 129. Sum Root to Leaf Numbers

## Description

 

Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path `1->2->3` which represents the number `123`.

Find the total sum of all root-to-leaf numbers.

**Note:** A leaf is a node with no children.

**Example:**

```
Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

**Example 2:**

```
Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

## Crack

通过preoder的遍历，每个`treeNode`对应一个`sum`，将`sum`一直传递

利用`sum = sum * 10 + root.val` 进行迭代计算

遍历到叶子时，用total将 `sum` 相加

## Solution

### Concise Version & not change ADT

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
    int total;
    
    public int sumNumbers(TreeNode root) {
        helper(root, 0);
        return total;
    }
    
    public void helper(TreeNode root, int sum) {
        if(root == null) return;
        sum = sum * 10 + root.val;
        if(root.right == null && root.left == null) total += sum;
        helper(root.left, sum);
        helper(root.right, sum);
    }
}
```



### First Try

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
    int total;
    
    public int sumNumbers(TreeNode root) {
        helper(root);
        return total;
    }
    
    public void helper(TreeNode root) {
        if(root == null) return;
        if(root.left != null) root.left.val = root.val * 10 + root.left.val;
        if(root.right != null) root.right.val = root.val * 10 + root.right.val;
        if(root.right == null && root.left == null) total += root.val;
        helper(root.left);
        helper(root.right);
    }
}
```



## Note

* 这里迭代的argument `sum`相当于建立了一个私有副本对应与每个node相对应