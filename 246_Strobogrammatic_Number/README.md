# 246. Strobogrammatic Number

## Description

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

**Example 1:**

```
Input:  "69"
Output: true
```

**Example 2:**

```
Input:  "88"
Output: true
```

**Example 3:**

```
Input:  "962"
Output: false
```

## Solution

```java
class Solution {
    public boolean isStrobogrammatic(String num) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        map.put('8', '8');
        map.put('1', '1');
        map.put('0', '0');
        map.put('6', '9');
        map.put('9', '6');
        int lo = 0, hi = num.length() - 1;
        while(lo <= hi) {
            char cLo = num.charAt(lo++);
            char cHi = num.charAt(hi--);
            if(!map.containsKey(cLo)) return false;
            if(map.get(cLo) != cHi) return false;
        }
        return true;
    }
}
```

