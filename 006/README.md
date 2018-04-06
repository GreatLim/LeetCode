# 6. ZigZag Conversion
## Description
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

```java
string convert(string text, int nRows);
```

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## Solution
```java
class Solution {
    public String convert(String s, int numRows) {
        String str = new String();
        int d = 2 * (numRows - 1);
        int index = 0;
        if(numRows == 1) return s;
        for(int i = 0; i< numRows; i++) {
            index = i;
            int mark = 0;
            while(index < s.length()) {
                if(i == 0 || i == numRows -1) {
                    str += s.charAt(index);
                    index += d;
                } else {
                    str += s.charAt(index);
                    if (mark == 0) {
                        index += d - 2 * i;
                    } else {
                        index += 2 * i;
                    }
                    mark = Math.abs(1  - mark);
                }
            }
        }
        return str;
    }
}
```
###Other Solution
```java
class Solution {
    public String convert(String s, int numRows) {
        char[] chars = s.toCharArray();
        int len = chars.length;
        int i = 0;
        StringBuilder sbs[] = new StringBuilder[numRows];
        for(int j = 0; j < numRows; j++) {
            sbs[j] = new StringBuilder();
        }
        while(i < len) {
            for(int j = 0; j < numRows && i < len; j++) {
                sbs[j].append(chars[i++]);
            }
            for(int j = numRows - 2; j >= 1 && i < len; j--) {
                sbs[j].append(chars[i++]);
            }
        }
        for(int j = 1; j < numRows; j++ ) {
            sbs[0].append(sbs[j]);
        }
        return sbs[0].toString();
    }
}
```

