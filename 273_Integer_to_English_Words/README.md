# 273. Integer to English Words

## Description

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 231 - 1.

**Example 1:**

```
Input: 123
Output: "One Hundred Twenty Three"
```

**Example 2:**

```
Input: 12345
Output: "Twelve Thousand Three Hundred Forty Five"
```

**Example 3:**

```
Input: 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**Example 4:**

```
Input: 1234567891
Output: "One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```

## Solution

### Most Voted

```java
class Solution {
    private final String[] LESS_THAN_20 = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    private final String[] TENS = {"", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    private final String[] THOUSANDS = {"", "Thousand", "Million", "Billion"};
    
    public String numberToWords(int num) {
        if(num == 0) return "Zero";
        String s = new String();
        int i = 0;
        while (num > 0) {
            if(num % 1000 != 0)
                s = helper(num % 1000) +THOUSANDS[i] + " " + s;
            i++;
            num /= 1000;
        }
        return s.trim();
    }
    
    public String helper(int num) {
        if(num == 0) return "";
        if(num < 20) return LESS_THAN_20[num] + " ";
        if(num < 100) return TENS[num / 10] + " " + helper(num % 10);
        else return helper(num / 100) + "Hundred " + helper(num % 100);
    }
}
```

### Easier to Implement

```java
class Solution {
    private final String[] LESS_THAN_10 = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"};
    private final String[] LESS_THAN_20 = {"Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    private final String[] LESS_THAN_100 = {"", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    
    public String numberToWords(int num) {
        if(num == 0) return "Zero";
        return helper(num).trim();
    }
    
    public String helper(int num) {
        if(num == 0) return "";
        if(num < 10) return LESS_THAN_10[num] + " ";
        if(num < 20) return LESS_THAN_20[num % 10] + " ";
        if(num < 100) return LESS_THAN_100[num / 10] + " " + helper(num % 10);
        if(num < 1000) return helper(num / 100) + "Hundred " + helper(num % 100);
        if(num < 1000000) return helper(num / 1000) + "Thousand " + helper(num % 1000);
        if(num < 1000000000) return helper(num / 1000000) + "Million " + helper(num % 1000000);
        else return helper(num / 1000000000) + "Billion " + helper(num % 1000000000);
    }
}
```

