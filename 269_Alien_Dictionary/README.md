# 269. Alien Dictionary

## Description

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of **non-empty** words from the dictionary, where **words are sorted lexicographically by the rules of this new language**. Derive the order of letters in this language.

**Example 1:**

```
Input:
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: "wertf"
```

**Example 2:**

```
Input:
[
  "z",
  "x"
]

Output: "zx"
```

**Example 3:**

```
Input:
[
  "z",
  "x",
  "z"
] 

Output: "" 

Explanation: The order is invalid, so return "".
```

**Note:**

1. You may assume all letters are in lowercase.
2. You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
3. If the order is invalid, return an empty string.
4. There may be multiple valid order of letters, return any one of them is fine.

 

## Solution

### BFS + Topological

```java
class Solution {
    public String alienOrder(String[] words) {
        HashMap<Character, HashSet<Character>> map = new HashMap<>();
        HashMap<Character, Integer> indegree = new HashMap<>();
        StringBuilder res = new StringBuilder();
        
        for (String word : words) {
            for (char c : word.toCharArray()) {
                indegree.put(c, 0);
            }
        }
        
        for (int i = 0; i < words.length - 1; i++) {
            String cur = words[i];
            String next = words[i + 1];
            int len = Math.min(cur.length(), next.length());
            for (int j = 0; j < len; j++) {
                char c1 = cur.charAt(j);
                char c2 = next.charAt(j);
                if (c1 != c2) {
                    HashSet<Character> set = map.getOrDefault(c1, new HashSet<>());
                    if(!set.contains(c2)) indegree.put(c2, indegree.get(c2) + 1);
                    set.add(c2);
                    map.put(c1, set);
                    break;
                }
            }
        }
        
        Queue<Character> q = new LinkedList<>();
        
        
        for (Character c : indegree.keySet()) {
            if (indegree.get(c) == 0) q.add(c);
        }
        
        while (!q.isEmpty()) {
            char v = q.poll();
            res.append(v);
            if(map.containsKey(v)) {
                for(char w: map.get(v)) {
                    indegree.put(w, indegree.get(w) - 1);
                    if(indegree.get(w) == 0) 
                      q.offer(w);
                }
            }
        }

        
        if(res.length() == indegree.size()) return res.toString();
        return "";
        
    }
}
```

