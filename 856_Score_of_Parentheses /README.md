# 856. Score of Parentheses

## Description

Given a balanced parentheses string `S`, compute the score of the string based on the following rule:

- `()` has score 1
- `AB` has score `A + B`, where A and B are balanced parentheses strings.
- `(A)` has score `2 * A`, where A is a balanced parentheses string.

 

**Example 1:**

```
Input: "()"
Output: 1
```

**Example 2:**

```
Input: "(())"
Output: 2
```

**Example 3:**

```
Input: "()()"
Output: 2
```

**Example 4:**

```
Input: "(()(()))"
Output: 6
```

 

**Note:**

1. `S` is a balanced parentheses string, containing only `(` and `)`.
2. `2 <= S.length <= 50`



## Solution

```java
class Solution {
    public int scoreOfParentheses(String S) {
        Stack<Integer> stack = new Stack<Integer>();
        int res = 0;
        for (int i = 0; i < S.length(); i++) {
            if (S.charAt(i) == '(') 
                stack.push(-1);
            else {
                int n = stack.pop();
                if(n == -1) 
                    stack.push(1);
                else {
                    int sum = 0;
                    while(n != -1) {
                        sum += n;
                        n = stack.pop();
                    }
                    stack.push(sum * 2);
                }
            }
        }
        while(!stack.isEmpty()) {
            res += stack.pop();
        }
        return res;
    }
}
```

