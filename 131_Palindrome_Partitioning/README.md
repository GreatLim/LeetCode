# 131. Palindrome Partitioning

## Description

Given a string *s*, partition *s* such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of *s*.

**Example:**

```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

## Solution

### Faster Version

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new LinkedList<>();
        backtrack(s, res, new LinkedList<String>(), 0);
        return res;
    }
    
    public void backtrack(String s, List<List<String>> res, LinkedList<String> temp, int start) {
        if(s.length() == start) {
            res.add(new LinkedList<String>(temp));
            return;
        }
        for(int i = start; i < s.length(); i++) {
            if(isPalindrome(s, start, i)) {
                temp.add(s.substring(start, i + 1));
                backtrack(s, res, temp, i + 1);
                temp.removeLast();
            }
        }
    }
    
    public boolean isPalindrome(String s, int lo, int hi) {
        while (lo < hi) {
            if(s.charAt(lo++) != s.charAt(hi--)) return false;
        }
        return true;
    }
}
```

### Fisrt Version

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new LinkedList<>();
        backtrack(s, res, new LinkedList<String>());
        return res;
    }
    
    public void backtrack(String s, List<List<String>> res, LinkedList<String> temp) {
        if(s.length() == 0) {
            res.add(new LinkedList<String>(temp));
            return;
        }
        for(int i = 0; i < s.length(); i++) {
            String str = s.substring(0, i + 1);
            if(isPalindrome(str)) {
                temp.add(str);
                backtrack(s.substring(i + 1), res, temp);
                temp.removeLast();
            }
        }
    }
    
    public boolean isPalindrome(String s) {
        int lo = 0, hi = s.length() - 1;
        while (lo < hi) {
            if(s.charAt(lo++) != s.charAt(hi--)) return false;
        }
        return true;
    }
}
```



## Note

if the input is "aab", check if [0,0] "a" is palindrome. then check [0,1] "aa", then [0,2] "aab".
While checking [0,0], the rest of string is "ab", use ab as input to make a recursive call.
![enter image description here](http://1.bp.blogspot.com/-3g_qWEIsyUI/VJR0Co__PcI/AAAAAAAAAfg/okeb7u1mZnI/s1600/test.png)

in this example, in the loop of i=l+1, a recursive call will be made with input = "ab".
Every time a recursive call is made, the position of l move right.

How to define a correct answer?
Think about DFS, if the current string to be checked (Palindrome) contains the last position, in this case "c", this path is a correct answer, otherwise, it's a false answer.

![enter image description here](http://i58.tinypic.com/2la69p2.png)

line 13: is the boundary to check if the current string contains the last element.
l>=s.length()

```java
public class Solution {
    public List<List<String>> partition(String s) {
       List<List<String>> res = new ArrayList<List<String>>();
       List<String> list = new ArrayList<String>();
       dfs(s,0,list,res);
       return res;
    }
    
    public void dfs(String s, int pos, List<String> list, List<List<String>> res){
        if(pos==s.length()) res.add(new ArrayList<String>(list));
        else{
            for(int i=pos;i<s.length();i++){
                if(isPal(s,pos,i)){
                    list.add(s.substring(pos,i+1));
                    dfs(s,i+1,list,res);
                    list.remove(list.size()-1);
                }
            }
        }
    }
    
    public boolean isPal(String s, int low, int high){
        while(low<high) if(s.charAt(low++)!=s.charAt(high--)) return false;
        return true;
    }
    
}
```