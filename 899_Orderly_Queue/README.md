# 899. Orderly Queue

## Description

A string `S` of lowercase letters is given.  Then, we may make any number of *moves*.

In each move, we choose one of the first `K` letters (starting from the left), remove it, and place it at the end of the string.

Return the lexicographically smallest string we could have after any number of moves.

 

**Example 1:**

```
Input: S = "cba", K = 1
Output: "acb"
Explanation: 
In the first move, we move the 1st character ("c") to the end, obtaining the string "bac".
In the second move, we move the 1st character ("b") to the end, obtaining the final result "acb".
```

**Example 2:**

```
Input: S = "baaca", K = 3
Output: "aaabc"
Explanation: 
In the first move, we move the 1st character ("b") to the end, obtaining the string "aacab".
In the second move, we move the 3rd character ("c") to the end, obtaining the final result "aaabc".
```

 

**Note:**

1. `1 <= K <= S.length <= 1000`
2. `S` consists of lowercase letters only.





## Solution

```java
class Solution {
    public String orderlyQueue(String S, int K) {
        if (K > 1) {
            char[] chars = S.toCharArray();
            Arrays.sort(chars);
            return new String(chars);
        }
        String min = S;
        String doubleS = S + S;
        for (int i = 1; i < S.length(); i++) {
            String temp = doubleS.substring(i, i + S.length());
            if(temp.compareTo(min) < 0) min = temp;
        }
        return min;
    }
}
```







## Note

**Intuition**:
First, this is string rotation.
`12345` -> `23451` -> `34512` -> `45123` -> `51234`
I use number instead of letters to make it clear.

If `K == 1`, we can only rotate the whole string.
There are `S.length` different states and
we return the lexicographically smallest string.

If `K > 1`, it means we can:

1. rotate the whole string,
2. rotate the whole string except the first letter.
   `012345` -> `023451` -> `034512` -> `045123` -> `051234`

We can rotate `i+1`th big letter to the start (method 1),
then rotate `i`th big letter to the end (method 2).
`2XXX01` -> `XXX012`

In this way, we can bubble sort the whole string lexicographically.
So just return sorted string.