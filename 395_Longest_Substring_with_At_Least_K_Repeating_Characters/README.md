# 395. Longest Substring with At Least K Repeating Characters 

## Description

Find the length of the longest substring **T** of a given string (consists of lowercase letters only) such that every character in **T** appears no less than *k* times.

**Example 1:**

```
Input:
s = "aaabb", k = 3

Output:
3

The longest substring is "aaa", as 'a' is repeated 3 times.
```

**Example 2:**

```
Input:
s = "ababbc", k = 2

Output:
5

The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```

## Crack

* 找到包含 `i` 个不同字母的 substring， 如果满足 `counter == i && counter == noLessThanK` 则进行更新
* 最终可判断满足

## Solution

```java
class Solution {
    public int longestSubstring(String s, int k) {
        HashMap<Character, Integer> map = new HashMap<>();
        HashSet<Character> set = new HashSet<>();
        int len = 0, n = 0;
        
       for (char c : s.toCharArray()) 
            set.add(c);
        
        n = set.size();
        
        for(int i = 1; i <= n; i++) {
            int lo = 0, hi = 0, counter = 0, noLessThanK = 0; 
            map = new HashMap<>();
            while (hi < s.length()) {
                char cHi = s.charAt(hi);
                map.put(cHi, map.getOrDefault(cHi, 0) + 1);
                if(map.get(cHi) == 1) counter++;
                if(map.get(cHi) == k) noLessThanK++;
                hi++;
                while(counter > i) {
                    char cLo = s.charAt(lo);
                    map.put(cLo, map.get(cLo) - 1);
                    if(map.get(cLo) == 0) counter--;
                    if(map.get(cLo) == k - 1) noLessThanK--;
                    lo++;
                }
                if(counter == i && counter == noLessThanK) len = Math.max(hi - lo, len);
            }
        }
        
        return len;
    }
}
```

