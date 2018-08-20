# 161. One Edit Distance

## Description

Given two strings **s** and **t**, determine if they are both one edit distance apart.

**Note:** 

There are 3 possiblities to satisify one edit distance apart:

1. Insert a character into **s** to get **t**
2. Delete a character from **s** to get **t**
3. Replace a character of **s** to get **t**

**Example 1:**

```
Input: s = "ab", t = "acb"
Output: true
Explanation: We can insert 'c' into s to get t.
```

**Example 2:**

```
Input: s = "cab", t = "ad"
Output: false
Explanation: We cannot get t from s by only one step.
```

**Example 3:**

```
Input: s = "1203", t = "1213"
Output: true
Explanation: We can replace '0' with '1' to get t.
```

## Solution

### Concise Version

```java
class Solution {
    public boolean isOneEditDistance(String s, String t) {
        int sl = s.length(), tl = t.length();
        int d = sl - tl;
        if (d == 0) {
            for(int i = 0; i < sl; i++) {
                char cs = s.charAt(i), ct = t.charAt(i);
                if(cs != ct) return s.substring(i + 1).equals(t.substring(i + 1));
            }
        } else if (d == 1) {
            return isDeleted(s, t);
        } else if (d == -1) {
            return isDeleted(t, s);
        }
        return false;
    }
    
    public boolean isDeleted(String s, String t) {
        int sl = s.length(), tl = t.length();
        for(int i = 0; i < tl; i++) {
                char cs = s.charAt(i), ct = t.charAt(i);
                if(cs != ct) return s.substring(i + 1).equals(t.substring(i));        
        }
        return true;
    }
}
```



### First Try

```java
class Solution {
    public boolean isOneEditDistance(String s, String t) {
        int sl = s.length(), tl = t.length();
        int d = sl - tl;
        if (d == 0) {
            int count = 0;
            for(int i = 0; i < sl; i++) {
                char cs = s.charAt(i), ct = t.charAt(i);
                if(cs != ct) count++;
            }
            return count == 1;
        } else if (d == 1) {
            return helper(s, t);
        } else if (d == -1) {
            return helper(t, s);
        }
        return false;
    }
    
    public boolean helper(String s, String t) {
        int sl = s.length(), tl = t.length();
        boolean deleted = false;
        if(tl == 0) return true;
        for(int i = 0, j = 0; i < sl && j < tl; i++, j++) {
            char cs = s.charAt(i);
            char ct = t.charAt(j);
            if(cs != ct) {
                if(!deleted) {
                    j--;
                    deleted = true;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}
```

