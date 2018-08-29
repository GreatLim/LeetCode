# 524. Longest Word in Dictionary through Deleting

## Description

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"
```

**Example 2:**

```
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"
```

**Note:**

1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.

## Solution

```java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        String res = "";
        int len = 0;
        for(String word : d) {
            if(helper(s.toCharArray(), word.toCharArray())) {
                if(word.length() > len) {
                    len = word.length();
                    res = word;
                } else if(word.length() == len && word.compareTo(res) < 0) {
                    res = word;
                }

            }
        }
        return res;
    }
    
    public boolean helper(char[] s, char[] word) {
        int i = 0, j = 0;
        int n = s.length, m = word.length;
        while(i < n && j < m) {
            char c1 = s[i], c2 = word[j];
            if(c1 == c2) {
                i++;
                j++;
            }
            else i++;
        }
        if(j == m) return true;
        return false;
    }
}
```

