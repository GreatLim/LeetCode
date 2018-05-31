# 56. Merge Intervals

## Description

Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considerred overlapping.
```



## Solution

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> res = new LinkedList<Interval>(); 
        if(intervals.size() == 0) return res;
        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval interval1, Interval interval2) {
                return interval1.start - interval2.start;
            }
        });
        int start = intervals.get(0).start;
        int end = intervals.get(0).end;

        for (Interval interval : intervals) {
            if(interval.start <= end) {
                end = Math.max(interval.end, end);
            } else {
                res.add(new Interval(start, end));
                start = interval.start;
                end = interval.end;
            }
        }
        res.add(new Interval(start, end));
        return res;
    }
}
```



## Notes

* Comparator can be directly defined in the method

  ``` java
          Collections.sort(intervals, new Comparator<Interval>(){
              public int compare(Interval interval1, Interval interval2) {
                  return interval1.start - interval2.start;
              }
          });
  ```

  ​

* Don't forget the last item

* List has its index, you can use get(0) to get the first element in list