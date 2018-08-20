# 498. Diagonal Traverse

##  Description

Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.

**Example:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output:  [1,2,4,7,5,3,6,8,9]
Explanation:
```

![img](https://leetcode.com/static/images/problemset/diagonal_traverse.png)

## Solution

```java
class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        if(matrix.length == 0 || matrix == null) return new int[0];
        int n = matrix.length, m = matrix[0].length;
        int[] res = new int[m * n];
        int i = 0, j = 0;
        for(int r = 0; r < res.length; r++) {
            res[r] = matrix[i][j];
            if((i + j) % 2 == 0) {
                if(j == m - 1) i++;
                else if(i == 0) j++;
                else {
                    i--; 
                    j++;
                }
            } else {
                if(i == n - 1) j++;
                else if(j == 0) i++;
                else {
                    i++; 
                    j--;
                }
            }
        }
        
        return res;
    }
}
```

