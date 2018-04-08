# 8. String to Integer (atoi)
## Description
Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

 

Requirements for atoi:

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.
## Solution
```java
class Solution {
    public int myAtoi(String str) {
        if(str.length() == 0) return 0;
        long result;
        int i = 0;
        int mark = 0;
        int start = 0;
        int end = 0;
        while(str.charAt(i) == ' ' && i < str.length()) {
            i++;
        }
        if(str.charAt(i) == '+') {
            i++;
        } else if(str.charAt(i) == '-') {
            mark = 1;
            i++;
        }
        start = i;
        while(i < str.length() && str.charAt(i) <= '9' && str.charAt(i) >= '0') {
            i++;
        }
        end = i;
        if(start == end) return 0;
        System.out.println(start);
        System.out.println(end);
        if(end - start > 10) end = start + 11;
        str = str.substring(start, end);
        result = (mark == 0) ? Long.parseLong(str) : - Long.parseLong(str);
        result = (result > Integer.MAX_VALUE) ? Integer.MAX_VALUE : result;
        result = (result < Integer.MIN_VALUE) ? Integer.MIN_VALUE : result;
        return (int) result;
    }
}
```

## Todo
* find the better way to solve the overflow.


