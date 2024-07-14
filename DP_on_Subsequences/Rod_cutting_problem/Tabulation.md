# Rod cutting Problem using Tabulation Approach

## Approach

For **tabulation(down -> top)**, first delcare the same dp array and base case. For base case, when **(ind == 0), N = 0,1,2,...., n**.

Then, turn the changing variable in the **loop**, i.e., **(1 -> n-1) for ind** and **(0 -> n) for N**. Then, **copy** the recursion and modify it.

## Code

```c++
    int cutRod(int price[], int n) {
        vector<vector<int>> dp(n, vector<int>(n+1 , 0));
        for(int i=0; i<=n; i++) dp[0][i] = i*price[0];

        for(int ind=1;ind<n;ind++){
            for(int j=0; j<=n;j++){
                int not_take = 0 + dp[ind-1][j];
                int take = INT_MIN;
                int rodLength = ind+1;
                if(rodLength <= j) take = price[ind] + dp[ind][j-rodLength];

                dp[ind][j] = max(take, not_take);
            }
        }
        return dp[n-1][n];
    }
```

**TC:** O(n\*n)

**SC:** O(n\*n)
