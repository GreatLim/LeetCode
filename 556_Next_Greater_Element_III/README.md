# 556. Next Greater Element III

## Description

Given a positive **32-bit** integer **n**, you need to find the smallest **32-bit** integer which has exactly the same digits existing in the integer **n**and is greater in value than n. If no such positive **32-bit** integer exists, you need to return -1.

**Example 1:**

```
Input: 12
Output: 21
```

 

**Example 2:**

```
Input: 21
Output: -1
```

## Solution

```java
class Solution {
    public int nextGreaterElement(int n) {
        char[] chars = String.valueOf(n).toCharArray();
        int i = 0, j = 0;
        for (i = chars.length - 2; i >= 0; i--) 
            if(chars[i] < chars[i + 1]) break;
        if(i == -1) return -1;
        for (j = chars.length - 1; j >= i; j--) 
            if(chars[j] > chars[i]) break;
        exchange(chars, i, j);
        reverse(chars, i + 1, chars.length - 1);
        
        long res = Long.parseLong(new String(chars));
        if(res >= Integer.MAX_VALUE) return -1;
        return (int) res;
    }
    
    public void exchange(char[] chars, int i, int j) {
        char temp = chars[i];
        chars[i] = chars[j];
        chars[j] = temp;
    }
    
    public void reverse(char[] chars, int lo, int hi) {
        while(lo < hi) {
            exchange(chars, lo++, hi--);
        }
    }
}
```

