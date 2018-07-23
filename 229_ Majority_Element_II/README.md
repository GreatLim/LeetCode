# 229. Majority Element II

## Description

Given an integer array of size *n*, find all elements that appear more than `n/3 ` times.

**Note:** The algorithm should run in linear time and in O(1) space.

**Example 1:**

```
Input: [3,2,3]
Output: [3]
```

**Example 2:**

```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

## Crack

* Boyer-Moore Majority Vote algorithm
* 最多有两个元素数量可以超过 1/3，所以设置两个候选数字
* 一定要先累加 `count` 再考虑更新 `candidate`

## Solution

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> list = new LinkedList();
        if(nums.length == 0 || nums == null) return list;
        int count1 = 0, candidate1 = nums[0], count2 = 0, candidate2 = nums[0];
        int limit = nums.length / 3;
        for(int num : nums) {
            if(num == candidate1) count1++;
            else if(num == candidate2) count2++;
            else if(count1 == 0) {
                candidate1 = num;
                count1 = 1;
            }
            else if(count2 == 0) {
                candidate2 = num;
                count2 = 1;
            }
            else {
                count1--;
                count2--;
            }
        }
        
        count1 = 0;
        count2 = 0;
        
        for(int num: nums) {
            if(num == candidate1) count1++;
            else if(num == candidate2) count2++;
        }
        if(count1 > limit) list.add(candidate1);
        if(count2 > limit) list.add(candidate2);
        return list;
    }
}
```



## Note

For those who aren't familiar with Boyer-Moore Majority Vote algorithm,
I found a great article (<http://goo.gl/64Nams>) that helps me to understand this fantastic algorithm!!
Please check it out!

The essential concepts is you keep a counter for the majority number **X**. If you find a number **Y** that is not **X**, the current counter should deduce 1. The reason is that if there is 5 **X** and 4 **Y**, there would be one (5-4) more **X** than **Y**. This could be explained as "4 **X** being paired out by 4 **Y**".

And since the requirement is finding the majority for more than ceiling of [n/3], the answer would be less than or equal to two numbers.
So we can modify the algorithm to maintain two counters for two majorities.

Followings are my sample Python code:

```python
class Solution:
# @param {integer[]} nums
# @return {integer[]}
def majorityElement(self, nums):
    if not nums:
        return []
    count1, count2, candidate1, candidate2 = 0, 0, 0, 1
    for n in nums:
        if n == candidate1:
            count1 += 1
        elif n == candidate2:
            count2 += 1
        elif count1 == 0:
            candidate1, count1 = n, 1
        elif count2 == 0:
            candidate2, count2 = n, 1
        else:
            count1, count2 = count1 - 1, count2 - 1
    return [n for n in (candidate1, candidate2)
                    if nums.count(n) > len(nums) // 3]
```