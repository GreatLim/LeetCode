# 139. Word Break

## Description

**Note:**

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

## Solution

### DP

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int len = s.length();
        boolean dp[] = new boolean[len + 1];
        dp[0] = true;
        for(int i = 0; i < len; i++) {
            if(dp[i]) {
                for(String word : wordDict) {
                    int end = i + word.length();
                    if(end <= len && s.substring(i, end).equals(word))
                        dp[end] = true;
                    if(dp[len]) return true;
                }
            }
        }
        return false;
    }
}
```



### First Try (Slow)

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if(s.length() == 0) return true;
        for(String word : wordDict) {
            if(word.length() <= s.length() && s.substring(0, word.length()).equals(word))
                if(wordBreak(s.substring(word.length()), wordDict)) return true;
        }
        return false;
    }
}
```

