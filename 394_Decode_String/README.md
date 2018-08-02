# 394. Decode String

## Description

Given an encoded string, return it's decoded string.

The encoding rule is: `k[encoded_string]`, where the *encoded_string* inside the square brackets is being repeated exactly *k* times. Note that *k* is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, *k*. For example, there won't be input like `3a` or `2[4]`.

**Examples:**

```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

## Solution

```java
class Solution {
    public String decodeString(String s) {
        if(s == null || s.length() == 0) return s;
        int num = 0;
        Stack<Integer> numStack = new Stack<>();
        Stack<String> strStack = new Stack<>();
        StringBuilder res = new StringBuilder();
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(Character.isDigit(c)) 
                num = num * 10 + c - '0';
            else {
                if(c == ']') {
                    String str = strStack.pop();
                    StringBuilder sb = new StringBuilder();
                    StringBuilder temp = new StringBuilder();
                    while(!str.equals("[")) {
                        temp.insert(0, str);
                        str = strStack.pop();
                    }
                    int size = numStack.pop();
                    for(int j = 0; j < size; j++) {
                        sb.append(temp);
                    }
                    strStack.push(sb.toString());
                } else {
                    strStack.push(Character.toString(c));
                    if(c == '[') {
                        numStack.push(num);
                        num = 0;
                    }
                }
            }
        }
        while(!strStack.isEmpty()) 
            res.insert(0, strStack.pop());
        return res.toString();
    }
}
```

