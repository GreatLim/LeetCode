# 508. Most Frequent Subtree Sum

## Description

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

**Examples 1**
Input:

```
  5
 /  \
2   -3
```

return [2, -3, 4], since all the values happen only once, return all of them in any order.

**Examples 2**
Input:

```
  5
 /  \
2   -5
```

return [2], since 2 happens twice, however -5 only occur once.

**Note:** You may assume the sum of values in any subtree is in the range of 32-bit signed integer.

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
    public int max = 0;
    public HashMap<Integer, Integer> map = new HashMap<>();
    public LinkedList<Integer> list = new LinkedList<>();
    
    public int[] findFrequentTreeSum(TreeNode root) {
        getSum(root);
        int[] res = new int[list.size()];
        for (int i = 0; i < res.length; i++) {
            res[i] = list.get(i);
        }
        return res;
    }
    
    public int getSum(TreeNode root) {
        if(root == null) return 0;
        int sum = root.val + getSum(root.left) + getSum(root.right);
        int freq = map.getOrDefault(sum, 0) + 1;
        map.put(sum, freq);
        if(freq == max) {
            list.add(sum);
        } else if(freq > max) {
            max = freq;
            list = new LinkedList<>();
            list.add(sum);
        }
        return sum;
    }
}
```

