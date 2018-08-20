# 247. Strobogrammatic Number II

## Description

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

**Example:**

```
Input:  n = 2
Output: ["11","69","88","96"]
```

## Solution

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        return helper(n, n);
    }
    
    public List<String> helper(int n, int m) {
        if(n == 0) return Arrays.asList("");
        if(n == 1) return Arrays.asList("0", "1", "8");
        
        List<String> list = helper(n - 2, m);
        List<String> res = new LinkedList<>();
        
        
        for(String s : list) {
            if(n != m) res.add("0" + s + "0");
            res.add("1" + s + "1");
            res.add("8" + s + "8");
            res.add("6" + s + "9");
            res.add("9" + s + "6");
        }
        return res;
    }
}
```

