# 760. Find Anagram Mappings

## Description

Given two lists `A`and `B`, and `B` is an anagram of `A`. `B` is an anagram of `A` means `B` is made by randomizing the order of the elements in `A`.

We want to find an *index mapping* `P`, from `A` to `B`. A mapping `P[i] = j` means the `i`th element in `A` appears in `B` at index `j`.

These lists `A` and `B` may contain duplicates. If there are multiple answers, output any of them.

For example, given

```
A = [12, 28, 46, 32, 50]
B = [50, 12, 32, 46, 28]
```

We should return `[1, 4, 3, 2, 0]` as `P[0] = 1` because the `0` th element of  `A`  appears at `B[1]`, and `P[1] = 4` because the `1` st element of  `A` appears at `B[4]`, and so on.

**Note:**

1. `A, B` have equal lengths in range `[1, 100]`.
2. `A[i], B[i]` are integers in range `[0, 10^5]`.



## Solution

```java
class Solution {
    public int[] anagramMappings(int[] A, int[] B) {
        int n = B.length;
        int[] res = new int[n];
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < n; i++) 
            map.put(B[i], i);
        for (int i = 0; i < n; i++) 
            res[i] = map.get(A[i]);
        return res;
    }
}
```

