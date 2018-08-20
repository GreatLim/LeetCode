# 721. Accounts Merge

## Description

Given a list `accounts`, each element `accounts[i]` is a list of strings, where the first element `accounts[i][0]` is a *name*, and the rest of the elements are *emails* representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some email that is common to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails **in sorted order**. The accounts themselves can be returned in any order.

**Example 1:**

```
Input: 
accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]]
Output: [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]
Explanation: 
The first and third John's are the same person as they have the common email "johnsmith@mail.com".
The second John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

**Note:**

The length of `accounts` will be in the range `[1, 1000]`.

The length of `accounts[i]` will be in the range `[1, 10]`.

The length of `accounts[i][j]` will be in the range `[1, 30]`.



## Solution

```java
class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        Map<String, String> owners = new HashMap<>();
        Map<String, String> parents = new HashMap<>();
        Map<String, TreeSet<String>> unions = new HashMap<>();
        List<List<String>> res = new LinkedList<>();
        for(List<String> a : accounts) {
            for(int i = 1; i < a.size(); i++) {
                owners.put(a.get(i), a.get(0));
                parents.put(a.get(i), a.get(i));
            }
        }
        for(List<String> a : accounts) {
            String p = find(a.get(1), parents);
            for(int i = 2; i < a.size(); i++) {
                parents.put(find(a.get(i), parents), p);
            }
        }
        for(List<String> a : accounts) {
            for(int i = 1; i < a.size(); i++) {
                String p = find(a.get(i), parents);
                if(!unions.containsKey(p)) 
                    unions.put(p, new TreeSet<>());
                unions.get(p).add(a.get(i));
            }
        }
        
        for(String p : unions.keySet()) {
            List<String> temp = new LinkedList<>(unions.get(p));
            temp.add(0, owners.get(p));
            res.add(temp);
        }
        return res;
        
    }
    
    public String find(String s, Map<String, String> parents) {
        String sParent = parents.get(s);
        if(sParent == s) return s;
        else return find(sParent, parents);
    }
}
```

