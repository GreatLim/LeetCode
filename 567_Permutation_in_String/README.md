# 567. Permutation in String

## Description

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

**Example 1:**

```
Input:s1 = "ab" s2 = "eidbaooo"
Output:True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

**Note:**

1. The input strings only contain lower case letters.
2. The length of both given strings is in range [1, 10,000].

## Solution

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        HashMap<Character, Integer> map = new HashMap<>();
        
        for(char c : s1.toCharArray()) 
            map.put(c, map.getOrDefault(c, 0) + 1);
        int lo = 0, hi = 0, counter = map.size();
        while(hi < s2.length()) {
            char cHi = s2.charAt(hi);
            if(map.containsKey(cHi)) {
                map.put(cHi, map.get(cHi) - 1);
                if(map.get(cHi) == 0) counter--;
            }
            hi++;
            while(counter == 0) {
                char cLo = s2.charAt(lo);
                if(map.containsKey(cLo)) {
                    map.put(cLo, map.get(cLo) + 1);
                    if(map.get(cLo) > 0) counter++;
                }
                if(hi - lo == s1.length()) return true;
                lo++;
            }
        }
        
        return false;
    }
}
```

