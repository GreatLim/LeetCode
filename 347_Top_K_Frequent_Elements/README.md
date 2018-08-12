# 347. Top K Frequent Elements

## Descritpion

Given a non-empty array of integers, return the **k** most frequent elements.

For example,
Given `[1,1,1,2,2,3]` and k = 2, return `[1,2]`.

**Note:** 

- You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than O(*n* log *n*), where *n* is the array's size.



## Solution

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        LinkedList<Integer> res = new LinkedList<>();
        LinkedList<Integer>[] buckets = new LinkedList[nums.length + 1];
        
        for(int num : nums) 
            map.put(num, map.getOrDefault(num, 0) + 1);
        
        for(int key : map.keySet()) {
            int freq = map.get(key);
            if(buckets[freq] == null) buckets[freq] = new LinkedList<>();
            buckets[freq].add(key);
        }
        
        
        int j = nums.length;
        for(int i = 0; i < k; i++) {
            while(buckets[j] == null || buckets[j].size() == 0) j--;
            res.add(buckets[j].remove());
        }
        return res;
    }
}
```

