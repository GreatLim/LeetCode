# 378. Kth Smallest Element in a Sorted Matrix

## Description

Given a *n* x *n* matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

**Note:** 
You may assume k is always valid, 1 ≤ k ≤ n2.



## Solution

### Binary Search

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int lo = matrix[0][0], hi = matrix[n - 1][n - 1] + 1;
        while (lo < hi) {
            int i = 0, j = n - 1, count = 0;
            int mid = lo + (hi - lo) / 2;
            while(i < n && j >= 0) {
                if(matrix[i][j] > mid) j--;
                else {
                    count += j + 1;
                    i++;
                }
            }
            if(count < k) lo = mid + 1;
            else hi = mid;
        }
        return lo;
    }
}
```



### Priority Queue

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<Tuple> pq = new PriorityQueue<>();
        int n = matrix.length;
        Tuple t = null;
        for(int j = 0; j < n; j++)
            pq.offer(new Tuple(0, j, matrix[0][j]));
        for(int i = 0; i < k; i++) {
            t = pq.poll();
            if(t.x == n - 1) continue;
            pq.offer(new Tuple(t.x + 1, t.y, matrix[t.x + 1][t.y]));
        }
        return t.val;
    }
    
    private class Tuple implements Comparable<Tuple> {
        private int x;
        private int y;
        private int val;
        
        private Tuple(int x, int y, int val) {
            this.x = x;
            this.y = y;
            this.val = val;
        }
        
        public int compareTo(Tuple t) {
            return this.val - t.val;
        }
    }
}
```



## Note

* 对于二分法 `int mid = lo + (hi - lo) / 2` 对于负数而言可以保证，`mid` 偏小



Solution 1 : Heap
Here is the step of my solution:

1. Build a minHeap of elements from the first row.
2. Do the following operations k-1 times :
   Every time when you poll out the root(Top Element in Heap), you need to know the row number and column number of that element(so we can create a tuple class here), replace that root with the next element from the same column.

After you finish this problem, thinks more :

1. For this question, you can also build a min Heap from the first column, and do the similar operations as above.(Replace the root with the next element from the same row)
2. What is more, this problem is exact the same with Leetcode373 Find K Pairs with Smallest Sums, I use the same code which beats 96.42%, after you solve this problem, you can check with this link:
   <https://discuss.leetcode.com/topic/52953/share-my-solution-which-beat-96-42>

```java
public class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        PriorityQueue<Tuple> pq = new PriorityQueue<Tuple>();
        for(int j = 0; j <= n-1; j++) pq.offer(new Tuple(0, j, matrix[0][j]));
        for(int i = 0; i < k-1; i++) {
            Tuple t = pq.poll();
            if(t.x == n-1) continue;
            pq.offer(new Tuple(t.x+1, t.y, matrix[t.x+1][t.y]));
        }
        return pq.poll().val;
    }
}

class Tuple implements Comparable<Tuple> {
    int x, y, val;
    public Tuple (int x, int y, int val) {
        this.x = x;
        this.y = y;
        this.val = val;
    }
    
    @Override
    public int compareTo (Tuple that) {
        return this.val - that.val;
    }
}
```

Solution 2 : Binary Search
We are done here, but let's think about this problem in another way:
The key point for any binary search is to figure out the "Search Space". For me, I think there are two kind of "Search Space" -- index and range(the range from the smallest number to the biggest number). Most usually, when the array is sorted in one direction, we can use index as "search space", when the array is unsorted and we are going to find a specific number, we can use "range".

Let me give you two examples of these two "search space"

1. index -- A bunch of examples -- <https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/> ( the array is sorted)
2. range -- <https://leetcode.com/problems/find-the-duplicate-number/> (Unsorted Array)

The reason why we did not use index as "search space" for this problem is the matrix is sorted in two directions, we can not find a linear way to map the number and its index.

```java
public class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int lo = matrix[0][0], hi = matrix[matrix.length - 1][matrix[0].length - 1] + 1;//[lo, hi)
        while(lo < hi) {
            int mid = lo + (hi - lo) / 2;
            int count = 0,  j = matrix[0].length - 1;
            for(int i = 0; i < matrix.length; i++) {
                while(j >= 0 && matrix[i][j] > mid) j--;
                count += (j + 1);
            }
            if(count < k) lo = mid + 1;
            else hi = mid;
        }
        return lo;
    }
}
```