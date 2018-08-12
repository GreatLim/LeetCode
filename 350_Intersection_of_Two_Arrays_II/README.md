# 350. Intersection of Two Arrays II

## Description

Given two arrays, write a function to compute their intersection.

**Example:**
Given *nums1* = `[1, 2, 2, 1]`, *nums2* = `[2, 2]`, return `[2, 2]`.

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

**Follow up:**

- What if the given array is already sorted? How would you optimize your algorithm?
- What if *nums1*'s size is small compared to *nums2*'s size? Which algorithm is better?
- What if elements of *nums2* are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?



## Solution

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        int n = nums1.length, m = nums2.length;
        HashMap<Integer, Integer> map = new HashMap<>();
        LinkedList<Integer> list = new LinkedList<>();
        for(int i = 0; i < n; i++)
            map.put(nums1[i], map.getOrDefault(nums1[i], 0) + 1);
        for(int i = 0; i < m; i++) {
            int left = map.getOrDefault(nums2[i], 0);
            if(left == 0) continue;
            else {
                list.add(nums2[i]);
                map.put(nums2[i], left - 1);
            }
        }
        int [] res = new int[list.size()];
        int i = 0;
        for(int num : list) {
            res[i++] = num;
        }

        return res;
    }
}
```

