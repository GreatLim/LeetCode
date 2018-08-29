# 125. Valid Palindrome

## Description

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**

```
Input: "A man, a plan, a canal: Panama"
Output: true
```

**Example 2:**

```
Input: "race a car"
Output: false
```

## Solution

```java
class Solution {
    public boolean isPalindrome(String s) {
        int n = s.length();
        int lo = 0, hi = n - 1;
        while (lo < hi) {
            while(lo < hi && !Character.isLetterOrDigit(s.charAt(lo))) lo++;
            while(lo < hi && !Character.isLetterOrDigit(s.charAt(hi))) hi--;
            if(lo == hi) break;
            char cLo = s.charAt(lo++), cHi = s.charAt(hi--);
            if(Character.isUpperCase(cLo)) cLo = Character.toLowerCase(cLo);
            if(Character.isUpperCase(cHi))  cHi = Character.toLowerCase(cHi);
            if(cLo != cHi) return false;
        }
        return true;
    }
}
```

