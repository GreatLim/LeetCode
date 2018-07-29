# 877. Stone Game

## Description

 Alex and Lee play a game with piles of stones.  There are an even number of piles **arranged in a row**, and each pile has a positive integer number of stones `piles[i]`.

The objective of the game is to end with the most stones.  The total number of stones is odd, so there are no ties.

Alex and Lee take turns, with Alex starting first.  Each turn, a player takes the entire pile of stones from either the beginning or the end of the row.  This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alex and Lee play optimally, return `True` if and only if Alex wins the game.

 

**Example 1:**

```
Input: [5,3,4,5]
Output: true
Explanation: 
Alex starts first, and can only take the first 5 or the last 5.
Say he takes the first 5, so that the row becomes [3, 4, 5].
If Lee takes 3, then the board is [4, 5], and Alex takes 5 to win with 10 points.
If Lee takes the last 5, then the board is [3, 4], and Alex takes 4 to win with 9 points.
This demonstrated that taking the first 5 was a winning move for Alex, so we return true.
```

 

**Note:**

1. `2 <= piles.length <= 500`
2. `piles.length` is even.
3. `1 <= piles[i] <= 500`
4. `sum(piles)` is odd.



## Solution

### DP - 2D

```java
class Solution {
    public boolean stoneGame(int[] piles) {
        int n = piles.length;
        int[][] dp = new int[n][n];
        for(int i = 0; i < n; i++) dp[i][i] = piles[i];
        for(int d = 1; d < n; d++) 
            for(int i = 0; i + d < n; i++) 
                dp[i][i+d] = Math.max(piles[i] - dp[i+1][i+d], piles[i+d] - dp[i][i+d - 1]);
        return dp[0][n-1] > 0;
    }
}
```

### Return True

```java
class Solution {
    public boolean stoneGame(int[] piles) {
        return true;
    }
}
```

## Note

### Approach 1: Just return true

Alex is first to pick pile.
`piles.length` is even, and this lead to an interesting fact:
Alex can always pick odd piles or always pick even piles!

For example,
If Alex wants to pick even indexed piles `piles[0], piles[2], ....., piles[n-2]`,
he picks first `piles[0]`, then Lee can pick either `piles[1]` or `piles[n - 1]`.
Every turn, Alex can always pick even indexed piles and Lee can only pick odd indexed piles.

In the description, we know that `sum(piles)` is odd.
If `sum(piles[even]) > sum(piles[odd])`, Alex just picks all evens and wins.
If `sum(piles[even]) < sum(piles[odd])`, Alex just picks all odds and wins.

So, Alex always defeats Lee in this game.

### Approach 2: 2D DP

* What if piles.length can be odd?
* What if we want to know exactly the diffenerce of score?

Then we need to solve it with DP.

`dp[i][j]` means the biggest number of stones you can get more than opponent picking piles in `piles[i] ~ piles[j]`.
You can first pick `piles[i]` or `piles[j]`.

1. If you pick `piles[i]`, your result will be `piles[i] - dp[i + 1][j]`
2. If you pick `piles[j]`, your result will be `piles[j] - dp[i][j - 1]`

So we get:
`dp[i][j] = max(piles[i] - dp[i + 1][j], piles[j] - dp[i][j - 1])`

