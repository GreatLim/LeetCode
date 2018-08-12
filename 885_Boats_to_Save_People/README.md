# 885. Boats to Save People

## Descritpion

The `i`-th person has weight `people[i]`, and each boat can carry a maximum weight of `limit`.

Each boat carries at most 2 people at the same time, provided the sum of the weight of those people is at most `limit`.

Return the minimum number of boats to carry every given person.  (It is guaranteed each person can be carried by a boat.)

 

**Example 1:**

```
Input: people = [1,2], limit = 3
Output: 1
Explanation: 1 boat (1, 2)
```

**Example 2:**

```
Input: people = [3,2,2,1], limit = 3
Output: 3
Explanation: 3 boats (1, 2), (2) and (3)
```

**Example 3:**

```
Input: people = [3,5,3,4], limit = 5
Output: 4
Explanation: 4 boats (3), (3), (4), (5)
```

**Note**:

- `1 <= people.length <= 50000`
- `1 <= people[i] <= limit <= 30000`

## Crack

* 只能坐两个人是关键
* 人数最多和最少搭配最有可能达到最优
* Two Pointer



## Solution

### Concise Version

```java
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        int lo = 0, hi = people.length - 1, count = 0;
        Arrays.sort(people);
        while(lo <= hi) {
            if(people[lo] + people[hi] <= limit) lo++;
            count++;
            hi--;
        }
        return count;
    }  
}
```

### First Version

```java
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        int lo = 0, hi = people.length - 1;
        int num = 0;
        Arrays.sort(people);
        while(lo < hi) {
            if(people[lo] + people[hi] <= limit) {
                num++;
                hi--;
                lo++;
            } else {
                num++;
                hi--;
            }
        }
        if(lo == hi) num++;
        return num;
    }  
```



## Note

### First Version

* `people[lo] + people[hi] <= limit` 这时候可以有两个人上船，`lo` 和 `hi` 分别移动到下一个人的index，船数增加
* `people[lo] + people[hi] <= limit` 这时候只有 `people[hi]` 可以上船，`hi` 分别移动到下一个人的index，船数增加
* 当 `lo` < `hi`  , 则还存在有人没上船，循环继续
* `lo == hi` 时，表示只有一个人没上船，船数增加



