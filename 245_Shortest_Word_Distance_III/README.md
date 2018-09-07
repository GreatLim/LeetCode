# 245. Shortest Word Distance III

## Description

Given a list of words and two words *word1* and *word2*, return the shortest distance between these two words in the list.

*word1* and *word2* may be the same and they represent two individual words in the list.

**Example:**
Assume that words = `["practice", "makes", "perfect", "coding", "makes"]`.

```
Input: word1 = “makes”, word2 = “coding”
Output: 1
Input: word1 = "makes", word2 = "makes"
Output: 3
```

**Note:**
You may assume *word1* and *word2* are both in the list.



## Solution

```java
class Solution {
    public int shortestWordDistance(String[] words, String word1, String word2) {
        int pos1 = -1, pos2 = -1, dis = Integer.MAX_VALUE;
        if(!word1.equals(word2))
            for(int i = 0; i < words.length; i++) {
                if(words[i].equals(word1)) pos1 = i;
                else if(words[i].equals(word2)) pos2 = i;
                if(pos1 != -1 && pos2 != -1) 
                    dis = Math.min(Math.abs(pos1 - pos2), dis);
            }
        else 
            for(int i = 0; i < words.length; i++) {
                if(words[i].equals(word1)) {
                    pos2 = pos1;
                    pos1 = i;
                }
                if(pos1 != -1 && pos2 != -1) 
                    dis = Math.min(Math.abs(pos1 - pos2), dis);
            }
        return dis;
    }
}
```

