# 244. Shortest Word Distance II

## Description

Design a class which receives a list of words in the constructor, and implements a method that takes two words *word1* and *word2* and return the shortest distance between these two words in the list. Your method will be called *repeatedly* many times with different parameters. 

**Example:**
Assume that words = `["practice", "makes", "perfect", "coding", "makes"]`.

```
Input: word1 = “coding”, word2 = “practice”
Output: 3
Input: word1 = "makes", word2 = "coding"
Output: 1
```

**Note:**
You may assume that *word1* **does not equal to** *word2*, and *word1* and *word2* are both in the list.

## Solution

```java
class WordDistance {
    HashMap<String, LinkedList<Integer>> map = new HashMap<>();

    public WordDistance(String[] words) {
        for (int i = 0; i < words.length; i++) {
            if(!map.containsKey(words[i])) map.put(words[i], new LinkedList<>());
            map.get(words[i]).add(i);
        }
    }
    
    public int shortest(String word1, String word2) {
        List<Integer> l1 = map.get(word1);
        List<Integer> l2 = map.get(word2);
        int res = Integer.MAX_VALUE;
        int i = 0, j = 0;
        while (i < l1.size() && j < l2.size()) {
            int index1 = l1.get(i), index2 = l2.get(j);
            res = Math.min(res, Math.abs(index1 - index2));
            if(index1 < index2) i++;
            else j++;
        }
        return res;
    }
}

/**
 * Your WordDistance object will be instantiated and called as such:
 * WordDistance obj = new WordDistance(words);
 * int param_1 = obj.shortest(word1,word2);
 */
```

