# 179. Largest Number

## Description

Given a list of non negative integers, arrange them such that they form the largest number.

**Example 1:**

```
Input: [10,2]
Output: "210"
```

**Example 2:**

```
Input: [3,30,34,5,9]
Output: "9534330"
```

**Note:** The result may be very large, so you need to return a string instead of an integer.

## Crack

* Comparator的构建只要考虑`s1 + s2`和`s2 + s1`的比较就可以了

## Solution

```java
class Solution {
    public String largestNumber(int[] nums) {
        String[] strs = new String[nums.length];
        String res = "";
        for(int i = 0; i < nums.length; i++) {
            strs[i] = Integer.toString(nums[i]);
        }
        Arrays.sort(strs, new Comparator<String>() {
            public int compare(String s1, String s2) {
                return (s1 + s2).compareTo(s2 + s1);
            }
        });
        if(strs[nums.length - 1].equals("0")) return "0";
        for(int i = nums.length - 1; i >= 0; i--) 
            res += strs[i];
        return res;
    }
    
}
```

