# Longest common Subsequence Problem using Tabulation Approach

## Approach

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in recursion, we had declared base case when **(ind1 < 0 || ind2 < 0)**, which will be not possible for tabulation due to **negation**, hence, we will do **index shifting** here, where base case becomes now **(ind1 == 0 || ind2 == 0)**.

Then, turn the changing variable in the **loop**, i.e., **(1 -> n) for string1** and **(0 -> m) for string2**. Then, **copy** the recursion and modify it.

## Code

```c++
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.length();
        int m = text2.length();
        vector<vector<int>> dp(n+1, vector<int>(m+1, -1));

        for(int ind2=0; ind2<=m; ind2++) dp[0][ind2] = 0;
        for(int ind1=0; ind1<=n; ind1++) dp[ind1][0] = 0;

        for(int ind1 = 1; ind1<=n; ind1++){
            for(int ind2=1; ind2<=m ;ind2++){
                if(text1[ind1-1] == text2[ind2-1]) dp[ind1][ind2] = 1 + dp[ind1-1][ind2-1];
                else dp[ind1][ind2] = max(dp[ind1-1][ind2], dp[ind1][ind2-1]);
            }
        }
        return dp[n][m];
    }
```

**TC:** O(n\*m)

**SC:** O(n\*m)
