# 763. Partition Labels

## Description

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example 1:**

```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

**Note:**

1. `S` will have length in range `[1, 500]`.
2. `S` will consist of lowercase letters (`'a'` to `'z'`) only.

 

## Solution

```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        List<Integer> res = new LinkedList<>();
        int[] map = new int[26];
        for (int i = 0; i < S.length(); i++) 
            map[S.charAt(i) - 'a'] = i;
        
        int start = 0, end = 0;
        for (int i = 0; i < S.length(); i++) {
            char c = S.charAt(i);
            end = Math.max(map[c - 'a'], end);
            if(i == end) {
                res.add(end - start + 1);
                start = end + 1;
            }
        }
        return res;
    }
}
```

