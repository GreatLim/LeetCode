# 888. Uncommon Words from Two Sentences

## Description

We are given two sentences `A` and `B`.  (A *sentence* is a string of space separated words.  Each *word* consists only of lowercase letters.)

A word is *uncommon* if it appears exactly once in one of the sentences, and does not appear in the other sentence.

Return a list of all uncommon words. 

You may return the list in any order.

 


**Example 1:**

```
Input: A = "this apple is sweet", B = "this apple is sour"
Output: ["sweet","sour"]
```

**Example 2:**

```
Input: A = "apple apple", B = "banana"
Output: ["banana"]
```

## Solution

```java
class Solution {
    public String[] uncommonFromSentences(String A, String B) {
        String C = A + " " + B;
        String[] wordsC = C.split(" ");
        LinkedList<String> res = new LinkedList<>();

        HashMap<String, Integer> map = new HashMap();

        for(String word : wordsC) 
            map.put(word, map.getOrDefault(word, 0) + 1);
        
        
        for(String word : map.keySet()) 
            if(map.get(word) == 1) res.add(word);
        
        return res.toArray(new String[0]);
    }
}
```

