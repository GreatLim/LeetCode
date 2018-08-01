# 654. Maximum Binary Tree

## Description

Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:

1. The root is the maximum number in the array.
2. The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
3. The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.

Construct the maximum tree by the given array and output the root node of this tree.

**Example 1:**

```
Input: [3,2,1,6,0,5]
Output: return the tree root node representing the following tree:

      6
    /   \
   3     5
    \    / 
     2  0   
       \
        1
```

**Note:**

1. The size of the given array will be in the range [1,1000].

## Solution

### Iterative version

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
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return constructMaximumBinaryTree(nums, 0, nums.length);
    }
    
    private TreeNode constructMaximumBinaryTree(int[] nums, int start, int end) {
        if(start == end) return null;
        int index = start;
        for(int i = start; i < end; i++) 
            index = (nums[i] > nums[index]) ? i : index;
        
        TreeNode newNode = new TreeNode(nums[index]);
        newNode.left = constructMaximumBinaryTree(nums, start, index);
        newNode.right = constructMaximumBinaryTree(nums, index + 1, end);
        
        return newNode;
    }
}
```

### Stack Version

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
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        Deque<TreeNode> stack = new LinkedList<>();
        for(int num : nums) {
            TreeNode n = new TreeNode(num);
            while(!stack.isEmpty() && stack.peek().val < num) {
                n.left = stack.pop();
            }
            if(!stack.isEmpty()) stack.peek().right = n;
            stack.push(n);
        }
         return stack.isEmpty() ? null : stack.removeLast();
    }
}
```



## Note

1. traverse the array once and create the node one by one. and use stack to store a `decreasing sequence`.
2. each step, we create a new curNode. compare to the peek of stack,
   2.a. keep popping the stack while (`stack.peek().val < curNode.val`), and set the last popping node to be curNode.left.
   Because the last one fulfilling the criteria is the largest number among curNode's left children. => `curNode.left = last pop node`
   2.b. after popping up all nodes that fulfill (`stack.peek().val < curNode.val`),
   thus (`stack.peek().val > curNode.val`), the `stack.peek()` is curNode's root => `peek.right = curNode`
3. return the bottom node of stack.