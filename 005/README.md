# 5. Longest Palindromic Substring

## Description

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"
Output: "bb"
```



## Solution

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length() == 0) return s;
        String max = s.substring(0, 1);
        for(int i = 0; i < s.length() - 1; i++) {
            String s1 = Palindrome(i, i, s);
            String s2 = Palindrome(i, i + 1, s);
            String temp = s1.length() > s2.length() ? s1 : s2;
            max = temp.length() > max.length() ? temp : max;
        }
        return max;
    }
    
    private String Palindrome(int left, int right, String s) {
        while( left > -1 &&  right < s.length() && s.charAt(left) == s.charAt(right)) {
            left --;
            right ++;
        }
        return s.substring(left + 1 , right);
    }
}
```

