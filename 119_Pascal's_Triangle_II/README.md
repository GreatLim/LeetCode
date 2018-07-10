# 119. Pascal's Triangle II

##  Description

------

Given a non-negative index *k* where *k* ≤ 33, return the *k*th index row of the Pascal's triangle.

Note that the row index starts from 0.

![img](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)
In Pascal's triangle, each number is the sum of the two numbers directly above it.

**Example:**

```
Input: 3
Output: [1,3,3,1]
```

**Follow up:**

Could you optimize your algorithm to use only *O*(*k*) extra space?

## Solution

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> pre = null;
        List<Integer> cur = null;
        for(int i = 0; i <= rowIndex; i++) {
            cur = new ArrayList<Integer>();
            for(int j = 0; j < i + 1; j++) {
                if(pre == null || j == 0 || j == i) cur.add(1);
                else cur.add(pre.get(j) + pre.get(j - 1));
            }
            pre = cur;
        }
        return cur;
    }
}
```

