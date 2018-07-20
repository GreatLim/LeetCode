# 211. Add and Search Word - Data structure design

##  Description

Design a data structure that supports the following two operations:

```
void addWord(word)
bool search(word)
```

search(word) can search a literal word or a regular expression string containing only letters `a-z` or `.`. A `.` means it can represent any one letter.

**Example:**

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

**Note:**
You may assume that all words are consist of lowercase letters `a-z`.

## Solution

```java
class WordDictionary {
    private final static int R = 26;
    private Node root;
    
    private class Node {
        private boolean mark;
        private Node[] next = new Node[26];
    }

    /** Initialize your data structure here. */
    public WordDictionary() {
        root = new Node();
    }
    
    /** Adds a word into the data structure. */
    public void addWord(String word) {
        root = addWord(root, word, 0);
    }
    
    private Node addWord(Node x, String word, int d) {
        if(x == null) x = new Node();
        if(d == word.length()) {
            x.mark = true;
            return x;
        }
        char c = word.charAt(d);
        x.next[c - 'a'] = addWord(x.next[c - 'a'], word, d + 1);
        return x;
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        return search(root, word, 0);
    }
    
    private boolean search(Node x, String word, int d) {
        if(x == null) return false;
        if(d == word.length()) return x.mark;
        char c = word.charAt(d);
        if(c != '.') return search(x.next[c - 'a'], word, d + 1);
        for (int i = 0; i < 26; i++) {
            if(search(x.next[i], word, d + 1)) return true;
        }
        return false;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

