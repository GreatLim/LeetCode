# 165. Compare Version Numbers

##  Description

Compare two version numbers *version1* and *version2*.
If `*version1* > *version2*` return `1;` if `*version1* < *version2*` return `-1;`otherwise return `0`.

You may assume that the version strings are non-empty and contain only digits and the `.` character.
The `.` character does not represent a decimal point and is used to separate number sequences.
For instance, `2.5` is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

**Example 1:**

```
Input: version1 = "0.1", version2 = "1.1"
Output: -1
```

**Example 2:**

```
Input: version1 = "1.0.1", version2 = "1"
Output: 1
```

**Example 3:**

```
Input: version1 = "7.5.2.4", version2 = "7.5.3"
Output: -1
```

## Solution

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] strs1 = version1.split("\\.");
        String[] strs2 = version2.split("\\.");
        int len = Math.max(strs1.length, strs2.length);
        for(int i = 0; i < len; i++) {
            int num1 = (i < strs1.length) ? Integer.parseInt(strs1[i]) : 0;
            int num2 = (i < strs2.length) ? Integer.parseInt(strs2[i]) : 0;
            if(num1 > num2) return 1;
            else if(num1 < num2) return -1;
        }
        return 0;
    }
}
```

## Note

* `\\.`作为`split`的变量