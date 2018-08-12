# 621. Task Scheduler

## Decription

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval **n** that means between two **same tasks**, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the **least** number of intervals the CPU will take to finish all the given tasks.

**Example 1:**

```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```

**Note:**

1. The number of tasks is in the range [1, 10000].
2. The integer n is in the range [0, 100].



## Solution

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] cnt = new int[26];
        int i;
        
        for(char task : tasks)
            cnt[task - 'A']++;
        
        Arrays.sort(cnt);
        
        for(i = 25; i >= 0; i--) 
            if(cnt[i] < cnt[25]) break;
    
        return Math.max(tasks.length, (cnt[25] - 1) * (n + 1) + 25 - i);
    }
}
```



 