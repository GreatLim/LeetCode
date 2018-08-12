# 345. Reverse Vowels of a String

## Description

Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**
Given s = "hello", return "holle".

**Example 2:**
Given s = "leetcode", return "leotcede".

**Note:**
The vowels does not include the letter "y".



## Solution

```java
class Solution {
    public String reverseVowels(String s) {
        int n = s.length();
        int lo = 0, hi = n - 1;
        char[] chars = s.toCharArray();
        HashSet<Character> set = new HashSet<>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');
        set.add('A');
        set.add('E');
        set.add('I');
        set.add('O');
        set.add('U');
        while(lo < hi) {
            if(lo == s.length() || hi == -1) break;
            char cLo = chars[lo], cHi = chars[hi];
            if(!set.contains(cLo)) lo++;
            if(!set.contains(cHi)) hi--;
            if(set.contains(cLo) && set.contains(cHi)) {
                char temp = chars[lo];
                chars[lo] = chars[hi];
                chars[hi] = temp;
                lo++;
                hi--;
            }
        }
        
        return new String(chars);
        
    }
}
```

