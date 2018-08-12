# 149. Max Points on a Line

## Decription

Given *n* points on a 2D plane, find the maximum number of points that lie on the same straight line.

**Example 1:**

```
Input: [[1,1],[2,2],[3,3]]
Output: 3
Explanation:
^
|
|        o
|     o
|  o  
+------------->
0  1  2  3  4
```

**Example 2:**

```
Input: [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
Explanation:
^
|
|  o
|     o        o
|        o
|  o        o
+------------------->
0  1  2  3  4  5  6
```



## crack

* 遍历每个点，看它和后面的每个点构成的直线上有多少个点
* 对每个点建立map，斜率是key
* 斜率要用分数的形式，不要用double的形式存
* 计算分数时先求分子分母的最大公约数gcd，再都除以gcd
* 根据如下面的gcd的方法，gcd不会为0
* 重合的点特殊处理
* 要包括需要计算点的本身



## Solution

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
class Solution {
    public int maxPoints(Point[] points) {
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        int n = points.length;
        int res = 0;
        for(int i = 0; i < n; i++) {
            int overlap = 0, max = 0;
            map.clear();
            for(int j = i + 1; j < n; j++) {
                int x = points[i].x - points[j].x;
                int y = points[i].y - points[j].y;
                if(x == 0 && y == 0) {
                    overlap++;
                    continue;
                }
                int gcd = gcd(x, y);
                x = x / gcd;
                y = y / gcd;
                String pos = x + "," + y;
                int count = map.getOrDefault(pos, 0) + 1;
                max = Math.max(count, max);
                map.put(pos, count);
            }
            res = Math.max(res, max + overlap + 1);
        }
        return res;
    }
    
    public int gcd(int a, int b) {
        if(b == 0) return a;
        else return gcd(b, a % b);
    }
}
```

