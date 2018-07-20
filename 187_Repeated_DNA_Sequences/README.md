# 187. Repeated DNA Sequences

## Description

 All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

**Example:**

```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

Output: ["AAAAACCCCC", "CCCCCAAAAA"]
```

## Crack

* 哈希大法好！

## Solution

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        Set<String> seen = new HashSet<String>(), repeated = new HashSet<String>();
        for(int i = 0; i < s.length() - 9; i++) { 
            String temp = s.substring(i, i + 10);
            if(seen.contains(temp)) repeated.add(temp);
            else seen.add(temp);
        }
        return new LinkedList(repeated);
    }
}
```

