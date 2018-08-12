# 438. Find All Anagrams in a String

## Description

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## Solution

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        HashMap<Character, Integer> map = new HashMap<>();
        LinkedList<Integer> res = new LinkedList<>();
        
        for (int i = 0; i < p.length(); i++)
            map.put(p.charAt(i), map.getOrDefault(p.charAt(i), 0) + 1);
        
        
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
                if (end - begin == p.length()) res.add(begin);
                    
                begin++;
            }
            
        }
        return res;
    }
}
```

