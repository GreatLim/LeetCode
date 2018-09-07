# 451. Sort Characters By Frequency

## Description

Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**

```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

**Example 2:**

```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```

**Example 3:**

```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

## Soluiton

```java
class Solution {
    public String frequencySort(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        StringBuilder sb = new StringBuilder();
        for (char c : s.toCharArray()) 
            map.put(c, map.getOrDefault(c, 0) + 1);
        
        LinkedList<Character>[] buckets = new LinkedList[s.length() + 1];
        
        for (char c : map.keySet()) {
            int freq = map.get(c);
            if(buckets[freq] == null) buckets[freq] = new LinkedList<>();
            buckets[freq].add(c);
        }
        
        for(int i = s.length(); i >= 1; i--) {
            if(buckets[i] != null) {
                for(char c : buckets[i]) {
                    for(int j = 0; j < i; j++) 
                        sb.append(c);
                }
            }
        }
        
        return sb.toString();
    }
}
```

