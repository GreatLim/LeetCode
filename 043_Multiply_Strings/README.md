# 43. Multiply Strings

## Descritption

Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

**Example 1:**

```
Input: num1 = "2", num2 = "3"
Output: "6"
```

**Example 2:**

```
Input: num1 = "123", num2 = "456"
Output: "56088"
```

**Note:**

1. The length of both `num1` and `num2` is < 110.
2. Both `num1` and `num2` contain only digits `0-9`.
3. Both `num1` and `num2` do not contain any leading zero, except the number 0 itself.
4. You **must not use any built-in BigInteger library** or **convert the inputs to integer** directly.

## Solution

```java
class Solution {
    public String multiply(String num1, String num2) {
        int n = num1.length(), m = num2.length();
        int[] pos = new int[n + m];
        for(int i = n - 1; i >= 0; i--) {
            for(int j = m - 1; j >= 0; j--) {
                int n1 = num1.charAt(i) - '0', n2 = num2.charAt(j) - '0';
                int p1 = i + j + 1, p2 = i + j;
                int sum = n1 * n2 + pos[p1];

                pos[p1] = sum % 10;
                pos[p2] += sum / 10;
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for(int p : pos) {
            if(sb.length() == 0 && p == 0) continue;
            sb.append(p);
        }
        return (sb.length() == 0) ? "0" : sb.toString();
    }
}
```

