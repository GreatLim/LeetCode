# 216. Combination Sum III

## Description

Find all possible combinations of **\*k*** numbers that add up to a number **\*n***, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

**Note:**

- All numbers will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**

```
Input: k = 3, n = 7
Output: [[1,2,4]]
```

**Example 2:**

```
Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```

## Solution

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        trackback(k, n, 1, res, new LinkedList());
        return res;
    }
    
    public void trackback(int k, int n, int start, List<List<Integer>> res, List<Integer> temp) {
        if(n < 0 || temp.size() > k) return;
        if(n == 0 && temp.size() == k) {
            res.add(new LinkedList(temp));
            return;
        }
        for(int i = start; i <= 9; i++) {
            temp.add(i);
            trackback(k, n - i, i + 1, res, temp);
            // System.out.println(temp);
            temp.remove(temp.size() - 1);
        }
    }
}
```

