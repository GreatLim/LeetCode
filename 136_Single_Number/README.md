# 136. Single Number

##  Description

Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```

## Crack

利用异或算符的可交换性

## Solution

### XOR

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num : nums) {
            res ^= num;
        }
        return res;
    }
}
```



### HashSet

```java
class Solution {
    public int singleNumber(int[] nums) {
        HashSet<Integer> set = new HashSet<Integer>();
        for(int num : nums) {
            if(set.contains(num)) set.remove(num);
            else set.add(num);
        }
        Object[] res = set.toArray();
        return (int) res[0];
    }
}
```

