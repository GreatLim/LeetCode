# 17. Letter Combinations of a Phone Number

##  Description

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example:**

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

## Solution

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        String[] strs = {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        List<String> list = new LinkedList<String>();
        for(int i = 0; i < digits.length(); i++) {
            int digit = digits.charAt(i) - '0';
            list = helper(list, strs[digit]);
        }
        return list;
    }
    
    private List<String> helper(List<String> list, String s) {
        List<String> res = new LinkedList<String>();
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(list.isEmpty()) res.add(String.valueOf(c));
            else {
                for(String str : list) {
                String newStr = str + c;
                res.add(newStr);
                }
            }
        }
        return res;
    }   
}
```

