# 91. Decode Ways

## Description

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a **non-empty** string containing only digits, determine the total number of ways to decode it.

**Example 1:**

```
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**

```
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```



## Solution

### DP

```java
class Solution {
    public int numDecodings(String s) {
        int n = s.length();
        int[] dp = new int[n + 1];
        dp[n] = 1;
        dp[n - 1] = s.charAt(n - 1) != '0' ? 1 : 0;
        for (int i = n - 2; i >= 0; i--) {
            if(s.charAt(i) == '0') continue;
            dp[i] += dp[i + 1];
            if(Integer.parseInt(s.substring(i, i + 2)) <= 26)
                dp[i] += dp[i + 2];                
        }
        return dp[0];
    }
}
```



### HashMap


```java
class Solution {
    HashMap<String, Integer> map = new HashMap<>(); 
    public int numDecodings(String s) {
        if(map.containsKey(s)) return map.get(s);
        if(!s.equals("") && s.charAt(0) == '0') return 0;
        if(s.equals("")) return 1;
        int res = 0;
        res += numDecodings(s.substring(1));
        if(s.length() >= 2 && Integer.parseInt(s.substring(0, 2)) <= 26) 
            res += numDecodings(s.substring(2));
        map.put(s, res);    
        return res;
    }
}
```

