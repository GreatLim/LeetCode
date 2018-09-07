# 573. Squirrel Simulation

## Description

 

minimal

 

 

one nut

 

**Example 1:**

```
Input: 
Height : 5
Width : 7
Tree position : [2,2]
Squirrel : [4,4]
Nuts : [[3,0], [2,5]]
Output: 12
Explanation:
```

**Note:**

1. All given positions won't overlap.
2. The squirrel can take at most one nut at one time.
3. The given positions of nuts have no order.
4. Height and width are positive integers. 3 <= height * width <= 10,000.
5. The given positions contain at least one nut, only one tree and one squirrel.

 



## Solution

```java
class Solution {
    public int minDistance(int height, int width, int[] tree, int[] squirrel, int[][] nuts) {
        int min = Integer.MAX_VALUE, res = 0;
        for (int[] nut : nuts) {
            int dis = distance(nut, tree);
            res += 2 * dis;
            min = Math.min(distance(nut, squirrel) - dis, min);
        }
        res += min;
        return res;
    }
    
    public int distance(int[] a, int[] b) {
        return Math.abs(a[0] - b[0]) + Math.abs(a[1] - b[1]);
    }
}
```

