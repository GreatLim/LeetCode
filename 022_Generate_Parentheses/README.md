# 22. Generate Parentheses

## Description
Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given *n* = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## Solution

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<String>();
        helper(list, "", 0, 0, n);
        return list;
    }
    
    public void helper(List<String> list, String str, int open, int close, int max) {
        if(open == max && close == max) {
            list.add(str);
        }
        if(open < max) {
            helper(list, str + "(", open + 1, close, max);
        }
        if(close < open) {
            helper(list, str + ")", open, close + 1, max);
        }
    }
    
}
```

### 

