# 365. Water and Jug Problem

## Description

You are given two jugs with capacities *x* and *y* litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactly *z* litres using these two jugs.

If *z* liters of water is measurable, you must have *z* liters of water contained within **one or both buckets** by the end.

Operations allowed:

- Fill any of the jugs completely with water.
- Empty any of the jugs.
- Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.

**Example 1:** (From the famous [*"Die Hard"* example](https://www.youtube.com/watch?v=BVtQNK_ZUJg))

```
Input: x = 3, y = 5, z = 4
Output: True
```

**Example 2:**

```
Input: x = 2, y = 6, z = 5
Output: False
```

## Solution

```java
class Solution {
    public boolean canMeasureWater(int x, int y, int z) {
        if(x + y < z) return false;
        if(z == 0) return true;
        if(x == 0 && y != 0) return z % y == 0;
        if(x != 0 && y == 0) return z % x == 0;
        if(x == 0 && y == 0) return false;
        return z % gcd(x, y) == 0;
    }
    
    public int gcd(int a, int b) {
        while(a % b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        System.out.println(b);
        return b;
    }
}
```

