# 32. Longest Valid Parentheses

## Description

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

**Example 2:**

```
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
```

## Solution

```java
class Solution {
    public int longestValidParentheses(String s) {
        int n = s.length();
        int[] dp = new int[n];
        int res = 0;
        for (int i = 1; i < n; i++) {
            if(s.charAt(i) == '(') dp[i] = 0;
            else {
                int index = i - 1 - dp[i - 1];
                if(s.charAt(i - 1) == '(') dp[i] = (i - 2 >= 0 ? dp[i - 2] : 0) + 2;
                else if(index >= 0 && s.charAt(index) == '(') dp[i] = dp[i - 1] + 2 + (index - 1 >= 0 ? dp[index - 1] : 0);
                res = Math.max(dp[i], res);
            }
        }
        return res;
    }
}
```

