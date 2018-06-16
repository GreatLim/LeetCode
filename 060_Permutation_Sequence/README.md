# 60. Permutation Sequence

## Descripiton

The set `[1,2,3,...,*n*]` contains a total of *n*! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for *n* = 3:

1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`

Given *n* and *k*, return the *k*th permutation sequence.

**Note:**

- Given *n* will be between 1 and 9 inclusive.
- Given *k* will be between 1 and *n*! inclusive.

**Example 1:**

```
Input: n = 3, k = 3
Output: "213"
```

**Example 2:**

```
Input: n = 4, k = 9
Output: "2314"
```



## Crack

确定在factorial[i] & factorial[i - 1]中的位置，即



## Solution

``` java
class Solution {
    public String getPermutation(int n, int k) {
        List<Integer> list = new LinkedList<Integer>();
        StringBuilder s = new StringBuilder();
        int[] factorial = new int[n+1];
        int index = 0;
        factorial[0] = 1;
        


        for(int i = 1; i <= n; i++) {
            list.add(i);
            factorial[i] = factorial[i - 1] * i;
        }

        for(int i = n; i >= 1; i--) {
            index = (k - 1) % factorial[i] / factorial[i - 1];
            s.append(list.get(index));
            list.remove(index);
        }
        return s.toString();
    }

}
```



## Note

- 使用factorial[i]来记录数组
- use an array to store a series of factorials