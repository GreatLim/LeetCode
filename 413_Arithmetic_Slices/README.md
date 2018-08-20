# 413. Arithmetic Slices

## Descritption

A sequence of number is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequence:

```
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```

The following sequence is not arithmetic.

```
1, 1, 2, 5, 7
```

 

A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.

A slice (P, Q) of array A is called arithmetic if the sequence:
A[P], A[p + 1], ..., A[Q - 1], A[Q] is arithmetic. In particular, this means that P + 1 < Q.

The function should return the number of arithmetic slices in the array A.

 

**Example:**

```
A = [1, 2, 3, 4]

return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.
```



## Solution

### First Try

```java
class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        int n = A.length;
        int res = 0;
        if(n == 0 || n == 1) return 0;
        int[] d = new int[n - 1];
        for(int i = 0; i < n - 1; i++) 
            d[i] = A[i + 1] - A[i];
        int start = 0, end = 0;
        while(end < n - 1) {
            if(d[end] == d[start]) end ++;
            else {
                int k = end - start -1;
                res += (1 + k) * k / 2;
                start = end;
            }
        }
        int k = end - start -1;
        res += (1 + k) * k / 2;
        
        return res;
    }
}
```

