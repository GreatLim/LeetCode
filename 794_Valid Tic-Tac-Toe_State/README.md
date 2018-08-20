# 794. Valid Tic-Tac-Toe State

## Description

A Tic-Tac-Toe board is given as a string array `board`. Return True if and only if it is possible to reach this board position during the course of a valid tic-tac-toe game.

The `board` is a 3 x 3 array, and consists of characters `" "`, `"X"`, and `"O"`.  The " " character represents an empty square.

Here are the rules of Tic-Tac-Toe:

- Players take turns placing characters into empty squares (" ").
- The first player always places "X" characters, while the second player always places "O" characters.
- "X" and "O" characters are always placed into empty squares, never filled ones.
- The game ends when there are 3 of the same (non-empty) character filling any row, column, or diagonal.
- The game also ends if all squares are non-empty.
- No more moves can be played if the game is over.

```
Example 1:
Input: board = ["O  ", "   ", "   "]
Output: false
Explanation: The first player always plays "X".

Example 2:
Input: board = ["XOX", " X ", "   "]
Output: false
Explanation: Players take turns making moves.

Example 3:
Input: board = ["XXX", "   ", "OOO"]
Output: false

Example 4:
Input: board = ["XOX", "O O", "XOX"]
Output: true
```

**Note:**

- `board` is a length-3 array of strings, where each string `board[i]` has length 3.
- Each `board[i][j]` is a character in the set `{" ", "X", "O"}`.

## Solution

```java
class Solution {
    public boolean validTicTacToe(String[] board) {
        int[] rows = new int[3];
        int[] cols = new int[3]; 
        int diagnal = 0, disDiagnal = 0, turn = 0;
        boolean oWin, xWin;
        
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 3; j++) {
                char c = board[i].charAt(j);
                if(c == ' ') continue; 
                int add = (c == 'X') ? 1 : -1;
                turn += add;
                rows[i] += add;
                cols[j] += add;
                if (i == j) diagnal += add;
                if (i + j == 2) disDiagnal += add;
            }
        }
        
        xWin = (rows[0] == 3 || cols[0] == 3 || rows[1] == 3 || cols[1] == 3
                || rows[2] == 3 || cols[2] == 3 || diagnal == 3 || disDiagnal == 3);
        oWin = (rows[0] == -3 || cols[0] == -3 || rows[1] == -3 || cols[1] == -3
                || rows[2] == -3 || cols[2] == -3 || diagnal == -3 || disDiagnal == -3);
        
        
        return (turn == 1 && xWin && !oWin) 
            || (turn == 0 && oWin && !xWin)
            || ((turn == 1 || turn == 0) && !xWin && !oWin);
    }
}
```

