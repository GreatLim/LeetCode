# 282. Expression Add Operators

## Description

Given a string that contains only digits `0-9` and a target value, return all possibilities to add **binary** operators (not unary) `+`, `-`, or `*`between the digits so they evaluate to the target value.

**Example 1:**

```
Input: num = "123", target = 6
Output: ["1+2+3", "1*2*3"] 
```

**Example 2:**

```
Input: num = "232", target = 8
Output: ["2*3+2", "2+3*2"]
```

**Example 3:**

```
Input: num = "105", target = 5
Output: ["1*0+5","10-5"]
```

**Example 4:**

```
Input: num = "00", target = 0
Output: ["0+0", "0-0", "0*0"]
```

**Example 5:**

```
Input: num = "3456237490", target = 9191
Output: []
```



## Solution

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> res = new LinkedList<>();
        helper(res, num, "", target, 0, 0, 0);
        return res;
    }
    
    public void helper(List<String> res, String num, String path, int target, int start, long val, long mul) {
        if (start == num.length()) {
            if (target == val) res.add(path);
            return;
        }
        
        for(int i = start; i < num.length(); i++) {
            if(i != start && num.charAt(start) == '0') break;
            long temp = Long.parseLong(num.substring(start, i + 1));
            if(start == 0) helper(res, num, path + temp, target, i + 1, val + temp, temp);
            else {
                helper(res, num, path + "+" + temp, target, i + 1, val + temp, temp);
                helper(res, num, path + "-" + temp, target, i + 1, val - temp, - temp);
                helper(res, num, path + "*" + temp, target, i + 1, val - mul + mul * temp, mul * temp);
            }
        }
    }
}
```



## Note

This problem has a lot of edge cases to be considered:

1. overflow: we use a long type once it is larger than Integer.MAX_VALUE or minimum, we get over it.
2. 0 sequence: because we can't have numbers with multiple digits started with zero, we have to deal with it too.
3. a little trick is that we should save the value that is to be multiplied in the next recursion.