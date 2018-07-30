# 4. Median of Two Sorted Arrays

## Description

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume **nums1** and **nums2** cannot be both empty.

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```



## Solution

### First Try

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n1 = nums1.length, n2 = nums2.length;
        if((n1 + n2) % 2 == 0) {
            return (getKth(nums1, 0, nums2, 0, (n1 + n2) / 2) + getKth(nums1, 0, nums2, 0, (n1 + n2) / 2 + 1)) * 0.5;
        }
        else
            return getKth(nums1, 0, nums2, 0, (n1 + n2) / 2 + 1);
    }
    
    public int getKth(int[] nums1, int start1, int[] nums2, int start2, int k) {
        int len1 = nums1.length - start1, len2 = nums2.length - start2;
        int d1 = Math.min(k / 2, len1), d2 = Math.min(k / 2, len2);
        int i1 = start1 + d1 - 1, i2 = start2 + d2 - 1;
        
        if(len2 < len1) return getKth(nums2, start2, nums1, start1, int k);
        if(len1 == 0) return nums2[start2 + k - 1];
        
        if(k == 1) return Math.min(nums1[start1], nums2[start2]);
        
        if(nums1[i1] < nums2[i2]) return getKth(nums1, start1 + d1, nums2, start2, k - d1);
        else return getKth(nums1, start1, nums2, start2 + d2, k - d2);
    }
    
}
```

### Note

## 解法三

上边的两种思路，时间复杂度都达不到题目的要求 O ( log ( m + n ) )。看到 log ，很明显，我们只有用到二分的方法才能达到。我们不妨用另一种思路，题目是求中位数，其实就是求第 k 小数的一种特殊情况，而求第 k 小数有一种算法。

解法二中，我们一次遍历就相当于去掉不可能是中位数的一个值，也就是一个一个排除。由于数列是有序的，其实我们完全可以一半儿一半儿的排除。假设我们要找第 k 小数，我们可以每次循环排除掉 k / 2 个数。看下边一个例子。

假设我们要找第 7 小的数字。

![img](http://pbs6qfi7i.bkt.clouddn.com/mid1.jpg)

我们比较两个数组的第 k / 2 个数字，如果 k 是奇数，向下取整。也就是比较第 3 个数字，上边数组中的 8 和 下边数组中的 3 ，如果哪个小，就表明该数组的前 k / 2 个数字都不是第 k 小数字，所以可以排除。也就是 1，2，3 这三个数字不可能是第 7 小的数字，我们可以把它排除掉。将 1389 和 45678910 两个数组作为新的数组进行比较。

更一般的情况 A [ 1 ]，A [ 2 ]，A [ 3 ]，A [ k / 2] … ，B[ 1 ]，B [ 2 ]，B [ 3 ]，B[ k / 2] … ，如果 A [ k / 2 ] < B [ k / 2 ] ，那么 A [ 1 ]，A [ 2 ]，A [ 3 ]，A [ k / 2] 都不可能是第 k 小的数字。

A 数组中比 A [ k / 2 ] 小的数有 k / 2 - 1 个，B 数组中，B [ k / 2 ] 比 A [ k / 2 ] 小，假设 B [ k / 2 ] 前边的数字都比 A [ k / 2 ] 小，也只有 k / 2 - 1 个，所以比 A [ k / 2 ] 小的数字最多有 k / 2 - 1 + k / 2 - 1 = k - 2 个，所以 A [ k / 2 ] 最多是第 k - 1 小的数。而比 A [ k / 2 ] 小的数更不可能是第 k 小的数了，所以可以把它们排除。

橙色的部分表示已经去掉的数字。

![img](http://pbs6qfi7i.bkt.clouddn.com/mid2.jpg)

由于我们已经排除掉了 3 个数字，就是这 3 个数字一定在最前边，所以在两个新数组中，我们只需要找第 7 - 3 = 4 小的数字就可以了，也就是 k = 4 。此时两个数组，比较第 2 个数字，3 < 5，所以我们可以把小的那个数组中的 1 ，3 排除掉了。

![img](http://pbs6qfi7i.bkt.clouddn.com/mid3.jpg)

我们又排除掉 2 个数字，所以现在找第 4 - 2 = 2 小的数字就可以了。此时比较两个数组中的第 k / 2 = 1 个数，4 = 4 ，怎么办呢？由于两个数相等，所以我们无论去掉哪个数组中的都行，因为去掉 1 个总会保留 1 个的，所以没有影响。为了统一，我们就假设 4 > 4 吧，所以此时将下边的 4 去掉。

![img](http://pbs6qfi7i.bkt.clouddn.com/mid4.jpg)

由于又去掉 1 个数字，此时我们要找第 1 小的数字，所以只需判断两个数组中第一个数字哪个小就可以了，也就是 4 。

所以第 7 小的数字是 4 。

我们每次都是取 k / 2 的数进行比较，有时候可能会遇到数组长度小于 k / 2 的时候。

![img](http://pbs6qfi7i.bkt.clouddn.com/mid5.jpg)

此时 k / 2 等于 3 ，而上边的数组长度是 2 ，我们此时将箭头指向它的末尾就可以了。这样的话，由于 2 < 3 ，所以就会导致上边的数组 1，2 都被排除。造成下边的情况。

![img](http://pbs6qfi7i.bkt.clouddn.com/mid6.jpg)

由于 2 个元素被排除，所以此时 k = 5 ，又由于上边的数组已经空了，我们只需要返回下边的数组的第 5 个数字就可以了。

从上边可以看到，无论是找第奇数个还是第偶数个数字，对我们的算法并没有影响，而且在算法进行中，k 的值都有可能从奇数变为偶数，最终都会变为 1 或者由于一个数组空了，直接返回结果。

所以我们采用递归的思路，为了防止数组长度小于 k / 2 ，所以每次比较 min ( k / 2，len ( 数组 ) ) 对应的数字，把小的那个对应的数组的数字排除，将两个新数组进入递归，并且 k 要减去排除的数字的个数。递归出口就是当 k = 1 或者其中一个数字长度是 0 了。

## 代码

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int n = nums1.length;
    int m = nums2.length;
    int left = (n + m + 1) / 2;
    int right = (n + m + 2) / 2;
    //将偶数和奇数的情况合并，如果是奇数，会求两次同样的 k 。
    return (getKth(nums1, 0, n - 1, nums2, 0, m - 1, left) + getKth(nums1, 0, n - 1, nums2, 0, m - 1, right)) * 0.5;  
}
    
    private int getKth(int[] nums1, int start1, int end1, int[] nums2, int start2, int end2, int k) {
        int len1 = end1 - start1 + 1;
        int len2 = end2 - start2 + 1;
        //让 len1 的长度小于 len2，这样就能保证如果有数组空了，一定是 len1 
        if (len1 > len2) return getKth(nums2, start2, end2, nums1, start1, end1, k);
        if (len1 == 0) return nums2[start2 + k - 1];

        if (k == 1) return Math.min(nums1[start1], nums2[start2]);

        int i = start1 + Math.min(len1, k / 2) - 1;
        int j = start2 + Math.min(len2, k / 2) - 1;

        if (nums1[i] > nums2[j]) {
            return getKth(nums1, start1, end1, nums2, j + 1, end2, k - (j - start2 + 1));
        }
        else {
            return getKth(nums1, i + 1, end1, nums2, start2, end2, k - (i - start1 + 1));
        }
    }
```

时间复杂度：每进行一次循环，我们就减少 k / 2 个元素，所以时间复杂度是 O（log（k）），而 k = （m + n）/ 2 ，所以最终的复杂也就是 O（log（m + n））。

空间复杂度：虽然我们用到了递归，但是可以看到这个递归属于尾递归，所以编译器不需要不停地堆栈，所以空间复杂度为 O（1）。

 