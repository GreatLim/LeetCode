# 526. Beautiful Arrangement

## Description

Suppose you have **N** integers from 1 to N. We define a beautiful arrangement as an array that is constructed by these **N** numbers successfully if one of the following is true for the ith position (1 <= i <= N) in this array:

1. The number at the ith position is divisible by **i**.
2. **i** is divisible by the number at the ith position.

Now given N, how many beautiful arrangements can you construct?

**Example 1:**

```
Input: 2
Output: 2
Explanation: 

The first beautiful arrangement is [1, 2]:

Number at the 1st position (i=1) is 1, and 1 is divisible by i (i=1).

Number at the 2nd position (i=2) is 2, and 2 is divisible by i (i=2).

The second beautiful arrangement is [2, 1]:

Number at the 1st position (i=1) is 2, and 2 is divisible by i (i=1).

Number at the 2nd position (i=2) is 1, and i (i=2) is divisible by 1.
```

**Note:**

1. **N** is a positive integer and will not exceed 15.



## Solution

```java
class Solution {
    int count = 0;
    public int countArrangement(int N) {
        backtrack(1, N, new boolean[N + 1]);
        return count;
    }
    
    public void backtrack(int i, int N, boolean[] used) {
        if (i > N) {
            count++;
            return;
        }
        for (int j = 1; j <= N; j++) {
            if(used[j]) continue;
            if(j % i == 0 || i % j == 0) {
                used[j] = true;
                backtrack(i + 1, N, used);
                used[j] = false;
            }
        }
    }
}
```

