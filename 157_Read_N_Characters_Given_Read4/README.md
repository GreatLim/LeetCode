# 157. Read N Characters Given Read4

## Description

The API: `int read4(char *buf)` reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the `read4` API, implement the function `int read(char *buf, int n)` that reads *n* characters from the file.

**Example 1:**

```
Input: buf = "abc", n = 4
Output: "abc"
Explanation: The actual number of characters read is 3, which is "abc".
```

**Example 2:**

```
Input: buf = "abcde", n = 5 
Output: "abcde"
```

**Note:**
The `read` function will only be called once for each test case.



## Solution

### Concise Verstion

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    public int read(char[] buf, int n) {
        int total = 0;
        char[] temp = new char[4];
        
        while(total < n) {
            int count = Math.min(read4(temp), n - total);
            for(int i = 0; i < count; i++)
                buf[total++] = temp[i];
            if(count < 4) break;
        }
        return total;
    }
}
```



### Most Voted

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    public int read(char[] buf, int n) {
        int total = 0;
        boolean eof = false;
        char[] temp = new char[4];
        
        while(!eof && total < n) {
            int count = Math.min(read4(temp), n - total);
            if(count < 4) eof = true;
            for(int i = 0; i < count; i++)
                buf[total++] = temp[i];
        }
        return total;
    }
}
```

