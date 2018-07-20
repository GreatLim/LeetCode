# 861. Score After Flipping Matrix

## Description

We have a two dimensional matrix `A` where each value is `0` or `1`.

A move consists of choosing any row or column, and toggling each value in that row or column: changing all `0`s to `1`s, and all `1`s to `0`s.

After making any number of moves, every row of this matrix is interpreted as a binary number, and the score of the matrix is the sum of these numbers.

Return the highest possible score.

 


**Example 1:**

```
Input: [[0,0,1,1],[1,0,1,0],[1,1,0,0]]
Output: 39
Explanation:
Toggled to [[1,1,1,1],[1,0,0,1],[1,1,1,1]].
0b1111 + 0b1001 + 0b1111 = 15 + 9 + 15 = 39
```

 

**Note:**

1. `1 <= A.length <= 20`
2. `1 <= A[0].length <= 20`
3. `A[i][j]` is `0` or `1`.

## Solution

```java
class Solution {
    public int matrixScore(int[][] A) {
        int n = A.length;
        int m = A[0].length;
        int score = 0;

        for(int i = 0; i < n; i++) 
            if(A[i][0] == 0) togRow(A, i);
        
        for(int j = 0; j < m; j++) {
            int sum = 0;
            for(int i = 0; i < n; i++)
                sum += A[i][j];
            if(sum * 2 < n) togCol(A, j);
        }

        for(int i = 0; i < n; i++) {
            int temp = 0;
            for(int j = 0; j < m; j++) {
                temp = 2 * temp + A[i][j];
                System.out.print(A[i][j] + " ");
            }
            score += temp;
            System.out.println();
        }
        
        return score;
    }
    
    public void togCol (int[][] A, int j) {
        int n = A.length;
        for(int i = 0; i < n; i++) 
            A[i][j] = (A[i][j] == 1) ? 0 : 1;
    }
    
    public void togRow (int[][] A, int i) {
        int m = A[0].length;
        for(int j = 0; j < m; j++) 
            A[i][j] = (A[i][j] == 1) ? 0 : 1;
    }
}
```

