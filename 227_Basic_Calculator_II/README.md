# 227. Basic Calculator II

## Description

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only **non-negative** integers, `+`, `-`, `*`, `/` operators and empty spaces ``. The integer division should truncate toward zero.

**Example 1:**

```
Input: "3+2*2"
Output: 7
```

**Example 2:**

```
Input: " 3/2 "
Output: 1
```

**Example 3:**

```
Input: " 3+5 / 2 "
Output: 5
```

**Note:**

- You may assume that the given expression is always valid.
- **Do not** use the `eval` built-in library function.

## Crack

* add `+` before the expression
* use `num` to track the current number
* use `sign` to record the operator. When meet a new operator
  * do some operations on current number
    * `+` & `-` : only need to push 
    * `*` & `\` : need previous number to calculate  a new number, then push it 
  * update `num` & `sign`
* corner case: 
  * case1: do the same operator when `i == s.length() - 1`
  * case2: do nothing when `c == ' '` , except case 1

## Solution

```java
class Solution {
    public int calculate(String s) {
        Stack<Integer> stack = new Stack<Integer>();
        char sign = '+';
        int num = 0, res = 0;
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(Character.isDigit(c)) {
                num = num * 10 + c - '0';
            }
            if(!Character.isDigit(c) && c != ' ' || i == s.length() - 1) {
                System.out.println(num);
                if(sign == '+') stack.push(num);
                else if(sign == '-') stack.push(-num);
                else if(sign == '*') stack.push(stack.pop() * num);
                else if(sign == '/') stack.push(stack.pop() / num);
                sign = c;
                num = 0;
            }
        }
        
        for(int i : stack) {
            res += i;
        }
        
        return res;
    }
}
```

