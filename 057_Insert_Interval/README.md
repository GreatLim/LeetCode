# 57. Insert Interval

## Description

Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

**Example 2:**

```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```



## Solution

### Concise Version

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
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> res = new LinkedList<Interval>();
        if(intervals.size() == 0) {
            res.add(newInterval);
            return res;
        }

        int i = 0;
        int start =  newInterval.start;
        int end = newInterval.end;
        while(i < intervals.size() && intervals.get(i).end < newInterval.start) {
            res.add(intervals.get(i++));
        }
        if(i < intervals.size()) start = Math.min(intervals.get(i).start, start);
        
        while(i < intervals.size() && intervals.get(i).start <= newInterval.end)
            end = Math.max(intervals.get(i++).end, end);
                
        res.add(new Interval(start, end));
            
        while(i < intervals.size())
            res.add(intervals.get(i++));
        
        return res;
    }
}
```

### First Try

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
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> res = new LinkedList<Interval>();
        if(intervals.size() == 0) {
            res.add(newInterval);
            return res;
        }
        int i = 0;
        int start =  newInterval.start;
        int end = newInterval.end;
        boolean isAdded = false;
        while(i < intervals.size()) {
            if(intervals.get(i).end < newInterval.start) 
                res.add(new Interval(intervals.get(i).start, intervals.get(i).end));
            else start = Math.min(intervals.get(i).start, start);
            
            if(intervals.get(i).start > newInterval.end) {
                if(!isAdded) {
                    res.add(new Interval(start, end));
                    isAdded = true;
                }
                res.add(new Interval(intervals.get(i).start, intervals.get(i).end));
            }
            else end = Math.max(intervals.get(i).end, end);
            i++;
        }
        if(!isAdded) {
            res.add(new Interval(start, end));
            isAdded = true;
        }
        return res;
    }
}
```



## Notes

* you can use index to iterate `List`

  `List.get(i)`
*  while and if, sometimes they can combine


## Todo

* make it consice