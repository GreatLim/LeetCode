# 31. Next Permutation

## Description
Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **in-place** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

`1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1`

## Solution
```java
class Solution {
    public void nextPermutation(int[] nums) {
        if(nums.length == 0) return;
        int i = nums.length - 1;
        while(i > 0) {
            if(nums[i - 1] < nums[i]) {
                break;
            }
            i--;
        }
        if(i == 0) {
            reverse(nums, 0, nums.length - 1);
            return;
        } 
        
        int minDiff = nums[i] - nums[i - 1];
        int j = i;
        for(int k = i + 1; k < nums.length; k++) {
            int diff = nums[k] - nums[i - 1];
            if(diff > 0 && diff <= minDiff) {
                minDiff = diff;
                j = k;
            }
        }
        swap(nums, i - 1, j);
        reverse(nums, i, nums.length - 1);
    }
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public void reverse(int[] nums, int start, int end) {
        for(int i = start, j = end; i <= (start + end) / 2; i++, j--) {
            swap(nums, i, j);
        }
    }
}
```

## Note

* remember to add **i++** or **i- -** in while(){}
* To reverse the array with the condition of start and end,  you need to check the distance from different sides