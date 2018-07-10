# 118. Pascal's Triangle

## Description

Given a non-negative integer *numRows*, generate the first *numRows* of Pascal's triangle.

![img](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)
In Pascal's triangle, each number is the sum of the two numbers directly above it.

**Example:**

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
] 
```

## Solution

### Better Solution

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        List<Integer> row = new LinkedList<Integer>();
        for(int i = 0; i < numRows; i++) {
            row.add(0, 1);
            for(int j = 1; j < i; j++) 
                row.set(j, row.get(j) + row.get(j + 1));
            res.add(new LinkedList<Integer>(row));
        }
        return res;
    }
}
```

## First Try

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> pre = null;
        List<Integer> cur = null;
        for(int i = 0; i < numRows; i++) {
            cur = new ArrayList<Integer>();
            for(int j = 0; j < i + 1; j++) {
                if(pre == null || j == 0 || j == i) cur.add(1);
                else cur.add(pre.get(j) + pre.get(j - 1));
            }
            res.add(cur);
            pre = cur;
        }
        return res;
    }
}
```

