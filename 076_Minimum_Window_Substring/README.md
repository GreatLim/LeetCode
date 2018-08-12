# 76. Minimum Window Substring

## Description

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**

```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

**Note:**

- If there is no such window in S that covers all characters in T, return the empty string `""`.
- If there is such window, you are guaranteed that there will always be only one unique minimum window in S.



## Solution


```java
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> map = new HashMap<>();
        String res = "";
        
        for (int i = 0; i < t.length(); i++)
            map.put(t.charAt(i), map.getOrDefault(t.charAt(i), 0) + 1);
        
        int len = Integer.MAX_VALUE;
        int counter = map.size();
        int end = 0, begin = 0;

        while (end < s.length()) {
            char cEnd = s.charAt(end);
            if (map.containsKey(cEnd)) {
                map.put(cEnd, map.get(cEnd) - 1);
                if (map.get(cEnd) == 0) counter--;
            }
            
            end++;
            
            while (counter == 0) {
                char cBegin = s.charAt(begin);
                if (map.containsKey(cBegin)) {
                    map.put(cBegin, map.get(cBegin) + 1);
                    if(map.get(cBegin) > 0) counter++;
                }
                if(end - begin < len) {
                    len = end - begin;
                    res = s.substring(begin, end);
                }
                begin++;
            }
            
        }
        return res;
    }
}
```

