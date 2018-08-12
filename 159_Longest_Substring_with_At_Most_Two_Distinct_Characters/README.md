# 159. Longest Substring with At Most Two Distinct Characters

## Description

Given a string **s** , find the length of the longest substring **t**  that contains **at most** 2 distinct characters.

**Example 1:**

```
Input: "eceba"
Output: 3
Explanation: t is "ece" which its length is 3.
```

**Example 2:**

```
Input: "ccaabbb"
Output: 5
Explanation: t is "aabbb" which its length is 5.
```

## Solution

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        int lo = 0, hi = 0, counter = 0, len = 0;
        while(hi < s.length()) {
            char cHi = s.charAt(hi);
            map.put(cHi, map.getOrDefault(cHi, 0) + 1);
            if(map.get(cHi) == 1) counter++;
            hi++;
            while(counter > 2) {
                char cLo = s.charAt(lo);
                map.put(cLo, map.get(cLo) - 1);
                if(map.get(cLo) == 0) counter--;
                lo++;
            }
            len = Math.max(len, hi - lo);
        }
        return len;
    }
}
```

