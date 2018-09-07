# 781. Rabbits in Forest

## Description

------

In a forest, each rabbit has some color. Some subset of rabbits (possibly all of them) tell you how many other rabbits have the same color as them. Those `answers` are placed in an array.

Return the minimum number of rabbits that could be in the forest.

```
Examples:
Input: answers = [1, 1, 2]
Output: 5
Explanation:
The two rabbits that answered "1" could both be the same color, say red.
The rabbit than answered "2" can't be red or the answers would be inconsistent.
Say the rabbit that answered "2" was blue.
Then there should be 2 other blue rabbits in the forest that didn't answer into the array.
The smallest possible number of rabbits in the forest is therefore 5: 3 that answered plus 2 that didn't.

Input: answers = [10, 10, 10]
Output: 11

Input: answers = []
Output: 0
```

**Note:**

1. `answers` will have length at most `1000`.
2. Each `answers[i]` will be an integer in the range `[0, 999]`.

## Solution

```java
class Solution {
    public int numRabbits(int[] answers) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int res = 0;
        for (int answer : answers) 
            map.put(answer, map.getOrDefault(answer, 0) + 1);
        for (int key : map.keySet()) {
            int value = map.get(key);
            res += value / (key + 1)  * (key + 1) + ((value % (key + 1) != 0) ? key + 1 : 0);
        }
        return res;
    }
}
```

