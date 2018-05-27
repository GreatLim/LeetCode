# 54. Spiral Matrix

## Description

Given a matrix of *m* x *n* elements (*m* rows, *n* columns), return all elements of the matrix in spiral order.

**Example 1:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

```
Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## Solution

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new LinkedList<Integer>();
        if(matrix.length == 0) return res;
        int rowBegin = 0, rowEnd = matrix.length - 1;
        int colBegin = 0, colEnd = matrix[0].length - 1;
        while(rowBegin <= rowEnd && colBegin <= colEnd) {
            for(int i = colBegin; i <= colEnd; i++) 
                res.add(matrix[rowBegin][i]);
            for(int i = rowBegin + 1; i <= rowEnd; i++) 
                res.add(matrix[i][colEnd]);
            if(rowBegin == rowEnd || colBegin == colEnd) break;
            for(int i = colEnd - 1; i > colBegin; i--)
                res.add(matrix[rowEnd][i]);
            for(int i = rowEnd; i > rowBegin; i--)
                res.add(matrix[i][colBegin]);
            rowBegin++;
            rowEnd--;
            colBegin++;
            colEnd--;
        }
        return res;
    }
}
```