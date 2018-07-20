# 208. Implement Trie (Prefix Tree)

## Descripition

Implement a trie with `insert`, `search`, and `startsWith` methods.

**Example:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

**Note:**

- You may assume that all inputs are consist of lowercase letters `a-z`.
- All inputs are guaranteed to be non-empty strings.

##  Solution

```java
class Trie {
    private static final int R = 26;
    private Node root;
    
    private class Node {
        private boolean mark = false;
        private Node[] next = new Node[R];
    }
    
    
    /** Initialize your data structure here. */
    public Trie() {
        root = new Node();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        root = insert(word, root, 0);
    }
    
    public Node insert(String word, Node x, int d) {
        if (x == null) x = new Node();
        if (d == word.length()) {
            x.mark = true;
            return x;
        }
        char c = word.charAt(d);
        int i = c - 'a';
        x.next[i] = insert(word, x.next[i], d + 1);
        return x;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Node x = get(word, root, 0);
        if(x == null) return false;
        else return x.mark;
    }
    
    public Node get(String word, Node x, int d) {
        if(x == null) return null;
        if(d == word.length()) return x;
        char c = word.charAt(d);
        int i = c - 'a';
        return get(word, x.next[i], d + 1);
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Node x = get(prefix, root, 0);
        return x != null;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

