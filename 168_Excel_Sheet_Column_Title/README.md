# 168. Excel Sheet Column Title

## Description

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```

**Example 1:**

```
Input: 1
Output: "A"
```

**Example 2:**

```
Input: 28
Output: "AB"
```

**Example 3:**

```
Input: 701
Output: "ZY"
```

## Crack

* 进制转换的问题
* `0 -> A` 变化为 `1 -> A`，所以 `n--`

## Solution

### Concise Version

```java
class Solution {
    public String convertToTitle(int n) {
        StringBuilder s = new StringBuilder();
        while (n > 0) {
            n--;
            int c = 'A' + n % 26;
            n = n / 26;
            s.insert(0, (char) c);
        }
        return s.toString();
    }
}
```

### First Try

```java
class Solution {
    public String convertToTitle(int n) {
        String s = "";
        while (n > 0) {
            int c = 'A' - 1 + ((n % 26 != 0) ? n % 26 : 26); 
            n = n / 26 - ((n % 26 != 0) ? 0 : 1);
            s = (char) c + s;
        }
        return s;
    }
}
```

