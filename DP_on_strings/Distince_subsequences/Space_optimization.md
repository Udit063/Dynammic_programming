# Distinct Subsequences Problem using Space Optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **prev** and **curr** and change accourdingly.

## Code

```c++
    int numDistinct(string s, string t) {
        int n = s.length();
        int m = t.length();

        vector<double> prev(m+1, 0), curr(m+1, 0);

        prev[0] = curr[0] = 1;

        for(int i=1; i<=n; i++){
            for(int j=1; j<=m; j++){
                if(s[i-1] == t[j-1]) curr[j] = prev[j-1] + prev[j];
                else curr[j] = prev[j];
            }
            prev = curr;
        }
        return (int)prev[m];
    }
```

**TC:** O(n\*m)

**SC:** O(m)
