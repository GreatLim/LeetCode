# 224. Basic Calculator

## Description

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, **non-negative** integers and empty spaces ``.

**Example 1:**

```
Input: "1 + 1"
Output: 2
```

**Example 2:**

```
Input: " 2-1 + 2 "
Output: 3
```

**Example 3:**

```
Input: "(1+(4+5+2)-3)+(6+8)"
Output: 23
```

Note:

- You may assume that the given expression is always valid.
- **Do not** use the `eval` built-in library function.

## Crack

* 使用` mark` 判断是否是新的 `num`

## Solution

### First Try

```java
class Solution {
    public int calculate(String s) {
        Stack<Character> ops = new Stack<Character>();
        Stack<Integer> vals = new Stack<Integer>();
        int num = 0;
        StringBuilder sb = new StringBuilder(s);
        sb.insert(0, '(');
        sb.append(')');
        s = sb.toString();
        boolean mark = false;;
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(Character.isDigit(c)) {
                num = num * 10 + c - '0';
                mark = true;
            } 
            if(!Character.isDigit(c) && c!= ' ') {
                if(c != '(' && mark) vals.push(num);
                if(c != ')') ops.push(c);
                if(c == ')'){
                    int temp = 0;
                    char op = ops.pop();
                    while(op != '(') {
                        if(op == '+') temp += vals.pop();
                        else temp -= vals.pop();
                        op = ops.pop();
                    }
                    temp += vals.pop();
                    vals.push(temp);
                    mark = false;
                }
                num = 0;
            }
        }
        return vals.pop();
    }
}
```



 