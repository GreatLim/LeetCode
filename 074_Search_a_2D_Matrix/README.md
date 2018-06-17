# 74. Search a 2D Matrix

## Description

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

**Example 1:**

```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
```

**Example 2:**

```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```

## Solution

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0) return false;
        int n = matrix[0].length, m = matrix.length;
        int lo = 0, hi = m * n - 1;
        while(lo <= hi) {
            int mid = (lo + hi) / 2;
            if(target == matrix[mid / n][mid % n]) return true;
            if(target < matrix[mid / n][mid % n]) hi = mid - 1;
            else lo = mid + 1;
        }
        return false;
    }
}
```

