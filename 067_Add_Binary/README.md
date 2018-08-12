# 67. Add Binary

## Description

Given two binary strings, return their sum (also a binary string).

The input strings are both **non-empty** and contains only characters `1` or `0`.

**Example 1:**

```
Input: a = "11", b = "1"
Output: "100"
```

**Example 2:**

```
Input: a = "1010", b = "1011"
Output: "10101"
```

 

## Solution

```java
class Solution {
    public String addBinary(String a, String b) {
        int aLen = a.length(), bLen = b.length(), i = 0, carry = 0;
        StringBuilder sb = new StringBuilder();
        while(i < aLen || i < bLen) {
            int num1 = (i < aLen) ? a.charAt(aLen - 1 - i) - '0' : 0;
            int num2 = (i < bLen) ? b.charAt(bLen - 1 - i) - '0' : 0;
            int sum = num1 + num2 + carry;
            int digit = sum % 2;
            carry = sum / 2;
            i++;
            sb.insert(0, digit);
        }
        if(carry != 0) sb.insert(0, carry);
        return sb.toString();
    }
}
```

