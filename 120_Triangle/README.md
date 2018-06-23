# 120. Triangle

## Description

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is `11` (i.e., **2** + **3** + **5** + **1** = 11).

**Note:**

Bonus point if you are able to do this using only *O*(*n*) extra space, where *n* is the total number of rows in the triangle.

## Solution

### First Try

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        List<Integer> dp = new ArrayList();
        int n = triangle.size();
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < n; i++) {
            List temp = new LinkedList<Integer>();
            for(int j = 0; j <= i; j++) {
                if(i == 0) temp.add(triangle.get(i).get(j));
                else {
                    int cur = triangle.get(i).get(j);
                    if(j == 0) temp.add(dp.get(0) + cur);
                    else if(i == j) temp.add(dp.get(i - 1) + cur);
                    else temp.add(Math.min(dp.get(j), dp.get(j - 1)) + cur);
                }
            }
            dp = temp;
        }
        for(int i : dp) {
            min = Math.min(min, i);
        }
        return min;
    }  
}
```



