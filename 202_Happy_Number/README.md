# 202. Happy Number

## Description

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example:** 

```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1 
```

## Solution

### Fast & Slow

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = next(n);
        int fast = next(next(n));
        while(slow != 1) {
            if(slow == fast) return false;
            slow = next(slow);
            fast = next(next(fast));
        }
        return true;
    }
    
    public int next(int n) {
        int sum = 0;
        while(n != 0) {
            sum += (n % 10) * (n % 10);
            n = n / 10;
        }
        return sum;
    }
}
```

### Set

```java
class Solution {
    public boolean isHappy(int n) {
        return helper(n, new HashSet<Integer>());
    }
    
    public boolean helper(int n, HashSet<Integer> set) {
        if(set.contains(n)) return false;
        else set.add(n);
        if(n == 1) return true;
        int sum = 0;
        while(n != 0) {
            sum += (n % 10) * (n % 10);
            n = n / 10;
        }
        return helper(sum, set);
    }
}
```

