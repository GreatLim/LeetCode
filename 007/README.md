# 7. Reverse Integer
## Description
Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

```
Input: 123
Output:  321
```

Example 2:

```
Input: -123
Output: -321
```
Example 3:

```
Input: 120
Output: 21
```

Note:
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Solution
```java
class Solution {
    public int reverse(int x) {
        int result = 0;
        while(x != 0) {
            int temp = result * 10 + x % 10;
            if((temp - x % 10) / 10 == result) {
                result = temp;
            } else {
                return 0;
            }
            x = x / 10;
        }
        return result;
    }
}
```
##Notes
* How to judge the integer overflow? (From CSAPP)

    Try to reverse the operation process and find out whether the result is the same.

    ```java
    // judge whether a + b is out of range.
    public boolean judgeOverflow(int a, int b) {
        int result;
        result = a + b;
        if(a == result - b) {
            return true;
        } else {
            return false;
        }
    }


