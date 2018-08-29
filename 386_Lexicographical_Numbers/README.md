# 386. Lexicographical Numbers

## Description

 Given an integer *n*, return 1 - *n* in lexicographical order.

For example, given 13, return: [1,10,11,12,13,2,3,4,5,6,7,8,9].

Please optimize your algorithm to use less time and space. The input size may be as large as 5,000,000.



## Solution

```java
class Solution {
    public List<Integer> lexicalOrder(int n) {
        LinkedList<Integer> res = new LinkedList<>();
        for(int i = 1; i <= 9; i++) 
            dfs(res, i, n);
        return res;
    }
    
    public void dfs(LinkedList<Integer> res, int num ,int n) {
        if(num > n) return;
        res.add(num);
        for(int i = 0; i <= 9; i++) 
            dfs(res, num * 10 + i, n);
    }
}
```

