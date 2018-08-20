# 368. Largest Divisible Subset

## Description

Given a set of **distinct** positive integers, find the largest subset such that every pair (Si, Sj) of elements in this subset satisfies: Si % Sj = 0 or Sj % Si = 0.

If there are multiple solutions, return any subset is fine.

**Example 1:**

```
nums: [1,2,3]

Result: [1,2] (of course, [1,3] will also be ok)
```

**Example 2:**

```
nums: [1,2,4,8]

Result: [1,2,4,8]
```

## Solution

### Faster Version - Use pre

```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        int[] dp = new int[n];
        int[] pre = new int[n];
        int max = 0, tail = -1;
        for (int i = 0; i < n; i++) {
            pre[i] = -1;
            dp[i] = 1;
            for (int j = 0; j < i; j++) {
                if(nums[i] % nums[j] == 0 && dp[j] + 1 > dp[i]) {
                    dp[i] = dp[j] + 1;
                    pre[i] = j;
                }
            }
            if(dp[i] > max) {
                max = dp[i];
                tail = i;
            }
        }
        LinkedList<Integer> res = new LinkedList<>();
        while(tail != -1) {
            res.add(nums[tail]);
            tail = pre[tail];
        }
        return res;
    }
}
```



### First Try

```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        List<List<Integer>> list = new LinkedList<>();
        List<Integer> res = new LinkedList<>();
        int size = 0;
        for (int i = 0; i < n; i++) {
            List<Integer> temp = new ArrayList<>();
            int sizeTemp = 0;
            for (int j = 0; j < i; j++) {
                if(list.get(j).size() > sizeTemp && nums[i] % nums[j] == 0) {
                    temp.clear();
                    temp.addAll(list.get(j));
                    sizeTemp = list.get(j).size();
                }
            }
            temp.add(nums[i]);
            list.add(temp);
            if(temp.size() > size) {
                res = temp;
                size = temp.size();
            }
        }
        return res;
    }
}
```

