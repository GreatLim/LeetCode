# 130. Surrounded Regions

### Description

Given a 2D board containing `'X'` and `'O'` (**the letter O**), capture all regions surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example:**

```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:

```
X X X X
X X X X
X X X X
X O X X
```

**Explanation:**

Surrounded regions shouldn’t be on the border, which means that any `'O'` on the border of the board are not flipped to `'X'`. Any `'O'` that is not on the border and it is not connected to an `'O'` on the border will be flipped to `'X'`. Two cells are connected if they are adjacent cells connected horizontally or vertically.

## Crack

从边界开始遍历用dfs，如果碰到'O'设置为'T'，最后再reset下 

## Solution

```java
class Solution {
    private char[][] board;
    private int n;
    private int m;
    public void solve(char[][] board) {
        if(board == null || board.length == 0) return;
        this.board = board;
        n = board[0].length;
        m = board.length;
        for(int i = 1; i < n - 1; i++) {
            if(board[0][i] == 'O') dfs(1, i);
            if(board[m - 1][i] == 'O') dfs(m - 2, i);
        }
        for(int j = 1; j < m - 1; j++) {
            if(board[j][0] == 'O') dfs(j, 1);
            if(board[j][n - 1] == 'O') dfs(j, n - 2);
        }
        reset();
    }
    
    public boolean isValid(int j, int i) {
        return i >= 0 && i < n && j >= 0 && j < m;
    }
    public boolean isBorder(int j, int i) {
        return i == 0 || i == n - 1 || j == 0 || j == m - 1;
    }
    
    public void dfs(int j, int i) {
        if(!isValid(j, i) || isBorder(j, i)) return;
        if(board[j][i] == 'X' || board[j][i] == 'T') return;
        if(board[j][i] == 'O') board[j][i] = 'T';
        dfs(j + 1, i);
        dfs(j - 1, i);
        dfs(j, i + 1);
        dfs(j, i - 1);
    }
    
    public void reset() {
        for(int i = 1; i < n - 1; i++) {
            for(int j = 1; j < m - 1; j++) {
                if(board[j][i] == 'O') board[j][i] = 'X';
                if(board[j][i] == 'T') board[j][i] = 'O';
            }
        }
    }
} 
```



## Note

* 以后统一一下二维数组中的变量
  * `n = nums.length`
  * `m = nums[0].length`
* 遍历时 `nums[i][j]`中`i`和`n`对应，`j`和`m`对应