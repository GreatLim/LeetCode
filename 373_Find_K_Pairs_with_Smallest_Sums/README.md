# 373. Find K Pairs with Smallest Sums

## Description

You are given two integer arrays **nums1** and **nums2** sorted in ascending order and an integer **k**.

Define a pair **(u,v)** which consists of one element from the first array and one element from the second array.

Find the k pairs **(u1,v1),(u2,v2) ...(uk,vk)** with the smallest sums.

**Example 1:**

```
Given nums1 = [1,7,11], nums2 = [2,4,6],  k = 3

Return: [1,2],[1,4],[1,6]

The first 3 pairs are returned from the sequence:
[1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

**Example 2:**

```
Given nums1 = [1,1,2], nums2 = [1,2,3],  k = 2

Return: [1,1],[1,1]

The first 2 pairs are returned from the sequence:
[1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

**Example 3:**

```
Given nums1 = [1,2], nums2 = [3],  k = 3 

Return: [1,3],[2,3]

All possible pairs are returned from the sequence:
[1,3],[2,3]
```

**Credits:**
Special thanks to [@elmirap](https://leetcode.com/elmirap/) and [@StefanPochmann](https://leetcode.com/stefanpochmann/) for adding this problem and creating all test cases. 



## Solution

```java
class Solution {
    public List<int[]> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        LinkedList<int[]> res = new LinkedList<>();
        int n = nums1.length, m = nums2.length;
        if(n == 0 || m == 0) return res;
        PriorityQueue<Tuple> pq = new PriorityQueue<Tuple>();
        Tuple t = null;
        
        for(int j = 0; j < m; j++) 
            pq.offer(new Tuple(0, j, nums1[0] + nums2[j]));
        
        for(int i = 0; i < k; i++) {
            if(pq.isEmpty()) break;
            t = pq.poll();
            res.add(new int[]{nums1[t.x], nums2[t.y]});
            if(t.x == n - 1) continue;
            pq.offer(new Tuple(t.x + 1, t.y, nums1[t.x + 1] + nums2[t.y]));
        }
        
        return res;
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

