# Wildcard Matching Problem using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in recursion, we had declared base case when **(i < 0 || j < 0)**, which will be not possible for tabulation due to **negation**, hence, we will do **index shifting** here, where base case becomes now **(i == 0 || j == 0)**.

Then, turn the changing variable in the **loop**, i.e., **(1 -> n) for p** and **(1 -> m) for s**. Then, **copy** the recursion and modify it.

## Code

```c++
    bool isMatch(string s, string p) {
        int m = s.size();
        int n = p.size();

        vector<vector<bool>> dp(n+1, vector<bool>(m+1, false));
        dp[0][0] = true;
        for(int j=1; j<=m; j++) dp[0][j] = false;
        for(int i=1; i<=n; i++){
            bool flag = true;
            for(int k=1; k<=i; k++){
                if(p[k-1] != '*'){
                    flag = false;
                    break;
                }
            }
            dp[i][0] = flag;
        }

        for(int i=1; i<=n; i++){
            for(int j=1; j<=m; j++){
                if(p[i-1] == s[j-1] || p[i-1] == '?') dp[i][j] = dp[i-1][j-1];
                else if(p[i-1] == '*') dp[i][j] = dp[i-1][j] | dp[i][j-1];
                else dp[i][j] = false;
            }
        }

        return dp[n][m];
    }
```

**TC:** O(n\*m)

**SC:** O(n\*m)
