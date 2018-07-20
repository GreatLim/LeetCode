# 858. Mirror Reflection

## Description

There is a special square room with mirrors on each of the four walls.  Except for the southwest corner, there are receptors on each of the remaining corners, numbered `0`, `1`, and `2`.

The square room has walls of length `p`, and a laser ray from the southwest corner first meets the east wall at a distance `q` from the `0`th receptor.

Return the number of the receptor that the ray meets first.  (It is guaranteed that the ray will meet a receptor eventually.)

 

**Example 1:**

```
Input: p = 2, q = 1
Output: 2
Explanation: The ray meets receptor 2 the first time it gets reflected back to the left wall.
```

**Note:**

1. `1 <= p <= 1000`
2. `0 <= q <= p`

 

## Solution

```java
class Solution {
    public int mirrorReflection(int p, int q) {
        int y = lcm(p, q) / p;
        int x = y / q * p;
        if(x % 2 == 0 && y % 2 != 0) return 2;
        if(x % 2 != 0 && y % 2 == 0) return 0;
        return 1;
        
    }
    
    public int gcd(int p, int q) {
        if(p % q == 0) return q;
        return gcd(q, p % q);
    }
    
    public int lcm(int p. int q) {
        return p * q / gcd(p, q);
    }
}
```

