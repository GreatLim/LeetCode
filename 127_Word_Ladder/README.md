# 127. Word Ladder

## Description

Given two words (*beginWord* and *endWord*), and a dictionary's word list, find the length of shortest transformation sequence from *beginWord* to *endWord*, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that *beginWord* is *not* a transformed word.

**Note:**

- Return 0 if there is no such transformation sequence.
- All words have the same length.
- All words contain only lowercase alphabetic characters.
- You may assume no duplicates in the word list.
- You may assume *beginWord* and *endWord* are non-empty and are not the same.

**Example 1:**

```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**

```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

##  Solution

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Queue<String> q = new LinkedList<String>();
        Set<String> visited = new HashSet<String>();
        Set dict = new HashSet<>(wordList);
        if(!dict.contains(endWord)) return 0;

        int level = 1;
        q.offer(beginWord);
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i = 0; i < size; i++) {
                String s1 = q.poll();
                visited.add(s1);
                for(int j = 0; j < s1.length(); j++) {
                    char[] chars = s1.toCharArray();
                    for(char c = 'a'; c < 'z'; c++) {
                        chars[j] = c;
                        String s2 = new String(chars);
                        if(dict.contains(s2)) {
                            if(!visited.contains(s2)) q.offer(s2);
                            dict.remove(s2);
                            if(s2.equals(endWord)) return level + 1;
                        }
                    }
                }
            }
            level++;
        }
        return 0;
    }
}
```

## Note

* `dict.remove(s2);` 可以大大优化时间