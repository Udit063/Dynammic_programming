# Distinct Subsequence Problem using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in recursion, we had declared base case when **(i < 0 || j < 0)**, which will be not possible for tabulation due to **negation**, hence, we will do **index shifting** here, where base case becomes now **(i == 0 || j == 0)**.

Then, turn the changing variable in the **loop**, i.e., **(1 -> n) for string1** and **(1 -> m) for string2**. Then, **copy** the recursion and modify it.

We need to change it in double, due to some runtime errors in some cases.

## Code

```c++
    int numDistinct(string s, string t) {
        int n = s.length();
        int m = t.length();
        vector<vector<double>> dp(n+1, vector<double>(m+1, 0));

        for(int i=0; i<=n; i++) dp[i][0] = 1;

        for(int i=1; i<=n; i++){
            for(int j=1; j<=m; j++){
                if(s[i-1] == t[j-1]) dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                else dp[i][j] = dp[i-1][j];
            }
        }
        return (int)dp[n][m];
    }
```

**TC:** O(n\*m)

**SC:** O(n\*m)
