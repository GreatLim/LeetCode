# 340. Longest Substring with At Most K Distinct Characters

## Description

Given a string, find the length of the longest substring T that contains at most *k* distinct characters.

**Example 1:**

```
Input: s = "eceba", k = 2
Output: 3
Explanation: T is "ece" which its length is 3.
```

**Example 2:**

```
Input: s = "aa", k = 1
Output: 2
Explanation: T is "aa" which its length is 2.
```

## Solution

```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        HashMap<Character, Integer> map = new HashMap<>();
        int lo = 0, hi = 0, counter = 0, len = 0;
        while(hi < s.length()) {
            char cHi = s.charAt(hi);
            map.put(cHi, map.getOrDefault(cHi, 0) + 1);
            if(map.get(cHi) == 1) counter++;
            hi++;
            while(counter > k) {
                char cLo = s.charAt(lo);
                map.put(cLo, map.get(cLo) - 1);
                if(map.get(cLo) == 0) counter--;
                lo++;
            }
            len = Math.max(len, hi - lo);
            System.out.println(lo + " " + hi);
        }
        return len;
    }
}
```

