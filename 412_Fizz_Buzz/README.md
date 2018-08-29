# 412. Fizz Buzz

## Description

Write a program that outputs the string representation of numbers from 1 to *n*.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

**Example:**

```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

## Solution

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        LinkedList<String> res = new LinkedList<>();
        for(int i = 1; i <= n; i++) {
            res.add(String.valueOf(i));
        }
        for(int i = 3; i <= n; i += 3) 
            res.set(i - 1, "Fizz");
        for(int i = 5; i <= n; i += 5) 
            res.set(i - 1, "Buzz");
        for(int i = 15; i <= n; i += 15) 
            res.set(i - 1, "FizzBuzz");
        return res;
    }
}
```

