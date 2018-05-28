# 55. Jump Game

## Description

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1:**

```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**

```
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```

## Solution

```java
class Solution {
    public boolean canJump(int[] nums) {
        int max = 0;
        for(int i = 0; i < nums.length - 1; i++) {
            max = Math.max(max, i + nums[i]);
            if(i == max) return false; //get stuck
        }
        return true;
    }
}
```

### Iterative Solution

```java
class Solution {
    public boolean canJump(int[] nums) {
        boolean[] isVisited = new boolean[nums.length];
        return jumpHelper(nums, isVisited, 0);
    }
    private boolean jumpHelper(int[] nums, boolean[] isVisited,int start) {
        isVisited[start] = true;
        if(start == nums.length - 1) return true;
        for(int i = nums[start]; i >= 1; i--) {
            if(start + i > nums.length - 1) return true;
            if(!isVisited[start + i] && jumpHelper(nums, isVisited, start + i)) return true;
        }
        return false;
    }
}
```

## Notes

* the natrue of this problem is figuring out the maximum reachable index. So we can set a variable max to reacord this reachable index. And when we jump to a new index, the only possible way that maximum reachable index can change is that the index add nums[index]
* if the maximum reachable index is equal to the index before the last index, this means that you get stuck and you have no chances to go to destination.