# 14. Longest Common Prefix

## Description
Write a function to find the longest common prefix string amongst an array of strings.

##Solution
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) return "";
        int end = strs[0].length();
        for(int i = 1; i < strs.length; i++) {
            end = Math.min(strs[i].length(), end);
            for(int j = 0; j < end && j < strs[i].length(); j++) {
                if(strs[i].charAt(j) != strs[0].charAt(j)) {
                    end = j;
                }
            }
        }
        return strs[0].substring(0, end);
    }
}
```

###Other Solutions

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
      if(strs == null || strs.length == 0)    return "";
      String pre = strs[0];
      int i = 1;
      while(i < strs.length){
          while(strs[i].indexOf(pre) != 0)
              pre = pre.substring(0,pre.length()-1);
          i++;
      }
      return pre;
  }
}
```



## Note

* indexOf() returns the begining index of the string, from where substring can match the argument