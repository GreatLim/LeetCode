# 884. Decoded String at Index

## Description

An encoded string `S` is given.  To find and write the *decoded* string to a tape, the encoded string is read **one character at a time** and the following steps are taken:

- If the character read is a letter, that letter is written onto the tape.
- If the character read is a digit (say `d`), the entire current tape is repeatedly written `d-1` more times in total.

Now for some encoded string `S`, and an index `K`, find and return the `K`-th letter (1 indexed) in the decoded string.

## Solution

```java
class Solution {
    public String decodeAtIndex(String S, int K) {
        long N = 0;
        for(int i = 0;i < S.length(); i++) {
            char c = S.charAt(i);
            N = Character.isDigit(c) ? (c - '0') * N : N + 1;
        }
        
        for(int i = S.length() - 1; i >= 0; i--) {
            char c = S.charAt(i);
            if(Character.isDigit(S.charAt(i))) {
                N /= c - '0';
                K %= N;
            } else if(K == 0 || K == N--)
                return String.valueOf(c);
        }
        return "";
    }
}
```

