# 79. Word Search

## Description

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

## Crack

这一题要使用DFS进行遍历

首先，我们需要寻找到DFS遍历的起点，也就是word第一个字符对应的位置

在进行DFS搜索的过程中，每当匹配到第一个字符，就将word缩短一格，对临近的4个方向再进行遍历。

**如果，临近的4个方向可以匹配，则继续。如果不行，则需要还原（trackback）。**

直到word为空时，我们可以确定，此时，成功匹配。

## Solution

### Concise Version (use trackback & dfs)

```java
class Solution {
    public char[][] board;
    public boolean[][] marked;
    public int n;
    public int m;
    
    public boolean exist(char[][] board, String word) {
        this.board = board;
        n = board.length;
        m = board[0].length;
        marked = new boolean[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if(board[i][j] == word.charAt(0) && dfs(i, j, word)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    public boolean dfs(int i, int j, String word) {
        if (word.isEmpty()) return true;
        if (i < 0 || i >= n || j < 0 || j >= m || marked[i][j] == true) return false;
        
        marked[i][j] = true;
        if(board[i][j] == word.charAt(0)) {
            word = word.substring(1);
            if(dfs(i + 1, j, word) || 
            dfs(i - 1, j, word) || 
            dfs(i, j + 1, word) || 
            dfs(i, j - 1, word)) {
                return true;
            }
        }
        marked[i][j] = false;
        return false;
    }
}
```

### trackback & dfs

```java
class Solution {
    public char[][] board;
    public boolean[][] marked;
    public int n;
    public int m;
    
    public boolean exist(char[][] board, String word) {
        this.board = board;
        n = board.length;
        m = board[0].length;
        boolean existed;
        marked = new boolean[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if(board[i][j] == word.charAt(0) && dfs(i, j, word)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    public boolean dfs(int i, int j, String word) {
        if (word.isEmpty()) return true;
        if (i < 0 || i >= n || j < 0 || j >= m || marked[i][j] || board[i][j] != word.charAt(0)) return false;
        marked[i][j] = true;
        word = word.substring(1);
        
        if(dfs(i + 1, j, word) || 
        dfs(i - 1, j, word) || 
        dfs(i, j + 1, word) || 
        dfs(i, j - 1, word)) {
            return true;
        } 
        
        marked[i][j] = false;
        return false;
    }
    
}
```

### Ugly Clone

``` java
class Solution {
    public char[][] board;
    public int n;
    public int m;
    
    public boolean exist(char[][] board, String word) {
        this.board = board;
        n = board.length;
        m = board[0].length;
        boolean existed;
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if(board[i][j] == word.charAt(0)) {
                    boolean[][] marked = new boolean[n][m];
                    existed = dfs(marked, i, j, word);
                    if(existed) return true;
                }
            }
        }
        return false;
    }
    
    public boolean dfs(boolean[][] marked, int i, int j, String word) {
        if (word.isEmpty()) return true;
        if (i < 0 || i >= n || j < 0 || j >= m || marked[i][j] == true || board[i][j] != word.charAt(0)) return false;
        marked[i][j] = true;
        word = word.substring(1);
        if(dfs(clone(marked), i + 1, j, word) || 
        dfs(clone(marked), i - 1, j, word) || 
        dfs(clone(marked), i, j + 1, word) || 
        dfs(clone(marked), i, j - 1, word)) {
            return true;
        } 
        // marked[i][j] = false;
        return false;
    }
    
    public boolean[][] clone(boolean[][] marked) {
        boolean[][] res = new boolean[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                res[i][j] = marked[i][j];
            }
        }
        return res;
    }
    
}
```
