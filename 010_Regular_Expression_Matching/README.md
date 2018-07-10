# 10. Regular Expression Matching

## Description

Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the **entire** input string (not partial).

**Note:**

- `s` could be empty and contains only lowercase letters `a-z`.
- `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

**Example 1:**

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

**Example 2:**

```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

**Example 3:**

```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

**Example 4:**

```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

**Example 5:**

```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

##  Solution

```java
class Solution {
    public boolean isMatch(String s, String p) {
        s = "0" + s;
        p = "0" + p;
        int n = s.length();
        int m = p.length();
        boolean[][] dp = new boolean[n][m];
        dp[0][0] = true;
        for(int i = 0; i < m; i++) {
            if(p.charAt(i) == '*' && dp[0][i - 2]) dp[0][i] = true;
        }
        for(int i = 1; i < n; i++) {
            for(int j = 1; j < m; j++) {
                if(p.charAt(j) == s.charAt(i) || p.charAt(j) == '.') 
                    dp[i][j] = dp[i - 1][j - 1];
                if(p.charAt(j) == '*') {
                    if(p.charAt(j - 1) == s.charAt(i) || p.charAt(j - 1) == '.') 
                        dp[i][j] = dp[i][j - 1] || dp[i][j - 2] || dp[i - 1][j];
                    else 
                        dp[i][j] = dp[i][j - 1] || dp[i][j - 2];
                }
            }
        }
        return dp[n - 1][m - 1];
    }
}
```

