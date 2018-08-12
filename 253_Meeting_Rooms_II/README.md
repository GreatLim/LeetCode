# 253. Meeting Rooms II

## Description

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...]` (si < ei), find the minimum number of conference rooms required.

**Example 1:**

```
Input: [[0, 30],[5, 10],[15, 20]]
Output: 2
```

**Example 2:**

```
Input: [[7,10],[2,4]]
Output: 1
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
    public int minMeetingRooms(Interval[] intervals) {
        if(intervals == null || intervals.length == 0) return 0;
        
        Arrays.sort(intervals, new Comparator<Interval>() {
            public int compare(Interval i1, Interval i2) {
                return i1.start - i2.start;
            }
        });
        
        PriorityQueue<Interval> pq = new PriorityQueue<>(new Comparator<Interval>() {
            public int compare(Interval i1, Interval i2) {
                return i1.end - i2.end;
            }
        });
        
        pq.offer(intervals[0]);
        
        for(int i = 1; i < intervals.length; i++) {
            Interval temp = pq.poll();
            if(intervals[i].start >= temp.end)
                temp.end = intervals[i].end;
            else pq.offer(intervals[i]);
            pq.offer(temp);
        }
        return pq.size();
    }
}
```

