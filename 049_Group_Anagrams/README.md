# 49. Group Anagrams

## Description

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.

## Solution

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map= new HashMap<String, List<String>>();
        for(String s: strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = String.valueOf(chars);
            if(!map.containsKey(key)) map.put(key, new ArrayList<String>());
            map.get(key).add(s);
        }
        return new ArrayList<List<String>>(map.values());
    }
}
```



## Notes

* String to char array

  `strStringType.toCharArray()`


* Char array to String

  `String.valueOf(chrCharArray )`

* use the collection to create a new list

  | Constructor and Description                                  |
  | ------------------------------------------------------------ |
  | `ArrayList()`Constructs an empty list with an initial capacity of ten. |
  | `ArrayList(Collection<? extends E> c)`Constructs a list containing the elements of the specified collection, in the order they are returned by the collection's iterator. |
  | `ArrayList(int initialCapacity)`Constructs an empty list with the specified initial capacity. |

  values

  ```
  public Collection<Object> values()
  ```

  Returns a Collection view of the attribute values contained in this Map.

  - Specified by:

    `values` in interface `Map<Object,Object>`

  - Returns:

    a collection view of the values contained in this map

* sort an array

  `Arrays.sort(chars)`