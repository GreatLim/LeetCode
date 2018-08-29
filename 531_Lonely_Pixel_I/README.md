# 531. Lonely Pixel I

## Description

------

Given a picture consisting of black and white pixels, find the number of **black** lonely pixels.

The picture is represented by a 2D char array consisting of 'B' and 'W', which means black and white pixels respectively.

A black lonely pixel is character 'B' that located at a specific position where the same row and same column don't have any other black pixels.

**Example:**

```
Input: 
[['W', 'W', 'B'],
 ['W', 'B', 'W'],
 ['B', 'W', 'W']]

Output: 3
Explanation: All the three 'B's are black lonely pixels.
```

**Note:**

1. The range of width and height of the input 2D array is [1,500].

## Solution

```java
class Solution {
    public int findLonelyPixel(char[][] picture) {
        int n = picture.length, m = picture[0].length, res = 0;
        int[] rows = new int[n], cols = new int[m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (picture[i][j] == 'B') {
                    rows[i]++;
                    cols[j]++;
                }
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (rows[i] == 1 && cols[j] == 1 && picture[i][j] == 'B') res++; 
            }
        }
        return res;
    }
}
```

