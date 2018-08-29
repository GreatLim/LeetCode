# 537. Complex Number Multiplication

## Description

Given two strings representing two [complex numbers](https://en.wikipedia.org/wiki/Complex_number).

You need to return a string representing their multiplication. Note i2 = -1 according to the definition.

**Example 1:**

```
Input: "1+1i", "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
```

**Example 2:**

```
Input: "1+-1i", "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```

**Note:**

1. The input strings will not have extra blank.
2. The input strings will be given in the form of **a+bi**, where the integer **a** and **b** will both belong to the range of [-100, 100]. And **the output should be also in this form**.

## Solution

```java
class Solution {
    public String complexNumberMultiply(String a, String b) {
        int[] numA = getXY(a);
        int[] numB = getXY(b);
        int x = numA[0] * numB[0] - numA[1] * numB[1];
        int y = numA[0] * numB[1] + numA[1] * numB[0];
        String res = x + "+" + y + "i";
        return res;
    }
    
    public int[] getXY(String s) {
        int[] res = new int[2];
        String[] nums = s.substring(0, s.length() - 1).split("\\+");
        res[0] = Integer.parseInt(nums[0]);
        res[1] = Integer.parseInt(nums[1]);
        return res;
    }
}
```

