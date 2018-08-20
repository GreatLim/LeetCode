# 399. Evaluate Division

## Description

Equations are given in the format `A / B = k`, where `A` and `B` are variables represented as strings, and `k` is a real number (floating point number). Given some queries, return the answers. If the answer does not exist, return `-1.0`.

**Example:**
Given `a / b = 2.0, b / c = 3.0.` 
queries are: `a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? .` 
return `[6.0, 0.5, -1.0, 1.0, -1.0 ].`

The input is: `vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries`, where `equations.size() == values.size()`, and the values are positive. This represents the equations. Return `vector<double>`.

According to the example above:

```
equations = [ ["a", "b"], ["b", "c"] ],
values = [2.0, 3.0],
queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ]. 
```

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.







```java
class Solution {
    HashMap<String, LinkedList<String>> map = new HashMap<>();
    HashMap<String, LinkedList<Double>> weights = new HashMap<>();
    
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        int n = equations.length, m = queries.length;
        double[] res = new double[m];
        for(int i = 0; i < n; i++) {
            String[] equation = equations[i];
            String v = equation[0], w = equation[1];
            double value = values[i];
            if(!map.containsKey(v)) {
                map.put(v, new LinkedList<>());
                weights.put(v, new LinkedList<>());
            }
            if(!map.containsKey(w)) {
                map.put(w, new LinkedList<>());
                weights.put(w, new LinkedList<>());
            }
            map.get(v).add(w);
            map.get(w).add(v);
            weights.get(v).add(value);
            weights.get(w).add(1 / value);
        }
        
        for(int i = 0; i < queries.length; i++) {
            String[] query = queries[i];
            String v = query[0], w = query[1];
            double temp = dfs(v, w, new HashSet<String>());
            if(temp != 0.0) res[i] = temp;
            else res[i] = -1.0;
        }
        return res;
    }
    
    public double dfs(String v, String w, HashSet<String> marked) {
        if(!map.containsKey(v) || !map.containsKey(w)) return 0.0;
        if(marked.contains(v)) return 0.0;
        if(v.equals(w)) return 1.0;
        marked.add(v);
        LinkedList<String> adjs = map.get(v);
        LinkedList<Double> nums = weights.get(v);
        double temp = 1.0;

        for(int i = 0; i < adjs.size(); i++) {
            temp = nums.get(i) * dfs(adjs.get(i), w, marked);
            if(temp != 0.0) return temp;
        }
        return 0.0;
    }
}
```

