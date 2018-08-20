# 128. Longest Consecutive Sequence

## Description

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(*n*) complexity.

**Example:**

```
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```



## Crack

* 由于数据之间没有连续，所以不考虑DP，可以用HashMap
* 遍历数组
  * 测试当前左右两边的数是否在HashMap中，获得目前包含有这两个数的最长连续数列的长度
  * 更新这串数列的最左和最右端HashMap中的长度



## Solution

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        int max = 0;
        for(int num : nums) {
            if(!map.containsKey(num)) {
                int left = map.getOrDefault(num - 1, 0);
                int right = map.getOrDefault(num + 1, 0);
                int sum = left + right + 1;
                map.put(num, sum);
                map.put(num - left, sum);
                map.put(num + right, sum);
                max = Math.max(sum, max);
            }
        }
        return max;
    }
}
```

