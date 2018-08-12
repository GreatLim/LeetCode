# 535. Encode and Decode TinyURL

## Description

> Note: This is a companion problem to the [System Design](https://leetcode.com/discuss/interview-question/system-design/) problem: [Design TinyURL](https://leetcode.com/discuss/interview-question/124658/Design-a-URL-Shortener-(-TinyURL-)-System/).

TinyURL is a URL shortening service where you enter a URL such as `https://leetcode.com/problems/design-tinyurl` and it returns a short URL such as `http://tinyurl.com/4e9iAk`.

Design the `encode` and `decode` methods for the TinyURL service. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.n



## Solution

```java
public class Codec {
    private static final String SEED_HOST = "http://tinyurl.com/";
    private static final String SEED = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    private HashMap<String, String> longToShort = new HashMap<>();
    private HashMap<String, String> shortToLong = new HashMap<>();


    // Encodes a URL to a shortened URL.
    public String encode(String longUrl) {
        if(longToShort.containsKey(longUrl)) 
            return longToShort.get(longUrl);
        
        String shortUrl = null;
        
        do{
            StringBuilder sb = new StringBuilder();
            for(int i = 0; i < 6; i++) {
                int pos = (int) (Math.random() * SEED.length());
                sb.append(SEED.charAt(pos));
            }
            shortUrl = sb.toString();
        } while(shortToLong.containsKey(shortUrl));
        
        longToShort.put(longUrl, shortUrl);
        shortToLong.put(shortUrl, longUrl);
        
        return SEED_HOST + shortUrl;
    }

    // Decodes a shortened URL to its original URL.
    public String decode(String shortUrl) {
        return shortToLong.get(shortUrl.replace(SEED_HOST, ""));
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(url));
```

