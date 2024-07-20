# Wildcard matching Problem using Space Optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **prev** and **curr** and change accourdingly.

## Code

```c++
    bool isMatch(string s, string p) {
        int m = s.size();
        int n = p.size();

        vector<bool> prev(m+1, false), curr(m+1, false);

        prev[0] = true;
        for(int j=1; j<=m; j++) prev[j] = false;

        for(int i=1; i<=n; i++){
            // at every first index of every column, we have to assign the 0th value of curr everytime
            bool flag = true;
            for(int k=1; k<=i; k++){
                if(p[k-1] != '*'){
                    flag = false;
                    break;
                }
            }

            //for every row, you are assigning the 0th col value
            curr[0] = flag;

            for(int j=1; j<=m; j++){
                if(p[i-1] == s[j-1] || p[i-1] == '?') curr[j] = prev[j-1];
                else if(p[i-1] == '*') curr[j] = prev[j] | curr[j-1];
                else curr[j] = false;
            }
            prev = curr;
        }
        return prev[m];
    }
```

**TC:** O(n\*m)

**SC:** O(m)
