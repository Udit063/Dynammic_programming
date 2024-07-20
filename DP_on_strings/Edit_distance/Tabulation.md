# Edit Distance Problem using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in recursion, we had declared base case when **(i < 0 || j < 0)**, which will be not possible for tabulation due to **negation**, hence, we will do **index shifting** here, where base case becomes now **(i == 0 || j == 0)**.

Then, turn the changing variable in the **loop**, i.e., **(1 -> n) for string1** and **(1 -> m) for string2**. Then, **copy** the recursion and modify it.

We need to change it in double, due to some runtime errors in some cases.

## Code

```c++
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>> dp(n+1, vector<int>(m+1, -1));

        for(int i=0; i<=n; i++) dp[i][0] = i;
        for(int j=0; j<=m; j++) dp[0][j] = j;

        for(int i=1; i<=n; i++){
            for(int j=1; j<=m; j++){
                if(word1[i-1] == word2[j-1]) dp[i][j] = 0 + dp[i-1][j-1];
                else{
                    int ins = 1 + dp[i][j-1];
                    int del = 1 + dp[i-1][j];
                    int rep = 1 + dp[i-1][j-1];

                    dp[i][j] = min(ins, min(del, rep));
                }
            }
        }
        return dp[n][m];
    }
```

**TC:** O(n\*m)

**SC:** O(n\*m)
