# 370. Range Addition

## Description

Assume you have an array of length **n** initialized with all **0**'s and are given **k** update operations.

Each operation is represented as a triplet: **[startIndex, endIndex, inc]** which increments each element of subarray **A[startIndex ... endIndex]** (startIndex and endIndex inclusive) with **inc**.

Return the modified array after all **k** operations were executed.

**Example:**

```
Given:

    length = 5,
    updates = [
        [1,  3,  2],
        [2,  4,  3],
        [0,  2, -2]
    ]

Output:

    [-2, 0, 3, 5, 3]
```

**Explanation:**

```
Initial state:
[ 0, 0, 0, 0, 0 ]

After applying operation [1, 3, 2]:
[ 0, 2, 2, 2, 0 ]

After applying operation [2, 4, 3]:
[ 0, 2, 5, 5, 3 ]

After applying operation [0, 2, -2]:
[-2, 0, 3, 5, 3 ]
```

**Credits:**
Special thanks to [@vinod23](https://discuss.leetcode.com/user/vinod23) for adding this problem and creating all test cases.



## Solution

```java
class Solution {
    public int[] getModifiedArray(int length, int[][] updates) {
        int[] temp = new int[length + 1];
        int[] res = new int[length];
        for (int i = 0; i < updates.length; i++) {
            int start = updates[i][0], end = updates[i][1], num = updates[i][2];
            temp[start] += num;
            temp[end + 1] -= num;
        }
        res[0] = temp[0];
        for (int i = 1; i < res.length; i++) {
            res[i] += res[i - 1] + temp[i]; 
        }
        return res;
    }
}
```

