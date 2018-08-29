# 805. Split Array With Same Average

## Descripiton

In a given integer array A, we must move every element of A to either list B or list C. (B and C initially start empty.)

Return true if and only if after such a move, it is possible that the average value of B is equal to the average value of C, and B and C are both non-empty.

```
Example :
Input: 
[1,2,3,4,5,6,7,8]
Output: true
Explanation: We can split the array into [1,4,5,8] and [2,3,6,7], and both of them have the average of 4.5.
```

**Note:**

- The length of `A` will be in the range [1, 30].
- `A[i]` will be in the range of `[0, 10000]`.





## Solution

```java
class Solution {
    public boolean splitArraySameAverage(int[] A) {
        int sum = 0;
        for (int num : A) 
            sum += num;
        
        boolean[][] dp = new boolean[sum + 1][A.length / 2 + 1];
        dp[0][0] = true;
        
        for(int num : A) {
            for(int i = sum; i >= num; i--) {
                for(int j = 1; j <= A.length / 2; j++) {
                    dp[i][j] = dp[i][j] || dp[i - num][j - 1];
                }
            }
        }
        
        for(int j = 1; j <= A.length / 2; j++) {
            if(sum * j % A.length == 0 && dp[sum * j / A.length][j]) return true;
        }
        
        return false;
    }
}
```

