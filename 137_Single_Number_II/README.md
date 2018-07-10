# 137. Single Number II

##  Description

Given a **non-empty** array of integers, every element appears *three* times except for one, which appears exactly once. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,3,2]
Output: 3
```

**Example 2:**

```
Input: [0,1,0,1,0,1,99]
Output: 99
```

## Solution 

### Bit Manipulation



### HashMap

```java
class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        int res = 0;
        for(int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
            if(map.get(num) <=2) res ^= num;
        }
        return res;
    }
}
```

## Todo

* Bit Manipulation Version

## Notes 

it's extremely difficult and tedious to see how the code functions by simply looking at it. Take a step back and consider what we need - to determine how many occurrences of an integer there are up to a maximum of three. We need to build a 3 state counter.

How do we do that? Boolean logic. Consider a single bit input and how that would drive the internal state of a bit counter in the state table below. An input value '0' does not change the internal state. Input of '1' drives the counter from state 0, 1, 2 and resets back to zero.

The state table can be implemented as a boolean circuit with two XOR, two AND, and two NOT gates. That construction is reflected in the solution code. Other constructions with identical functionality are also possible.

```
/* 3-state counter */
'A'  'twos'  'ones'    'twos'  'ones'
 0      0       0    |    0       0
 0      0       1    |    0       1
 0      1       0    |    1       0
 1      0       0    |    0       1
 1      0       1    |    1       0
 1      1       0    |    0       0

  for (int i = 0; i < A.size(); i++) {
    ones = (ones ^ a[i]) & ~twos;
    twos = (twos ^ a[i]) & ~ones;
  }
```

We can extend the same approach to a 4-state counter, which works on the same problem if we want to find a single occurrence among multiple occurrences of 4 values. The state table extends by one count before resetting, and we have a new set of boolean logic. Again, other boolean constructions are possible for the same state table.

For 5 states we would need to add a third bit as a 'threes' variable and additional logic design.

```
/* 4-state counter */
'A'  'twos'  'ones'    'twos'  'ones'
 0      0       0    |    0       0
 0      0       1    |    0       1
 0      1       0    |    1       0
 0      1       1    |    1       1
 1      0       0    |    0       1
 1      0       1    |    1       0
 1      1       0    |    1       1
 1      1       1    |    0       0

  for (int i = 0; i < A.size(); i++) {
    ones = (ones ^ A[i]);
    twos = (twos | A[i]) & (~A[i] | (ones ^ twos));
  }
```

Now here's the problem. The boolean code, which is the logic representation of the state table, is practically unreadable and gets substantially worse as the table grows. Going backwards from the boolean code to the state table is extremely painful and tedious - like disassembling machine code.

This solution is basically the result of a human compiler. Definitely novel, but practical? I'm thinking not so much. So don't worry if you can't understand the code immediately by simply looking at it. Nobody can.