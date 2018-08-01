# 297. Serialize and Deserialize Binary Tree

## Description

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Example:** 

```
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "[1,2,3,null,null,4,5]"
```

**Clarification:** The above format is the same as [how LeetCode serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        buildSerialize(root, sb);
        return sb.toString();
    }
    
    public void buildSerialize(TreeNode root, StringBuilder sb) {
        if(root == null) {
            sb.append("X").append(",");
        } else {
            sb.append(root.val).append(",");
            buildSerialize(root.left, sb);
            buildSerialize(root.right, sb);
        }
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Deque<String> dq = new LinkedList<>(Arrays.asList(data.split(",")));
        return buildDeserialize(dq);
    }
    
    public TreeNode buildDeserialize(Deque<String> dq) {
        if(dq.isEmpty()) return null;
        String s = dq.remove();
        if(s.equals("X")) return null;
        TreeNode n = new TreeNode(Integer.parseInt(s));
        n.left = buildDeserialize(dq);
        n.right = buildDeserialize(dq);
        return n;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

## Note

```
    1
   / \
  2   3
     / \
    4   5
```

**Your input**

```
[1,2,3,null,null,4,5]
```

##### Your stdout

```
1,2,X,X,3,4,X,X,5,X,X,
```

##### 