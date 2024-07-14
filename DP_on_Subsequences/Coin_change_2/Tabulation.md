# Ways to make coin change Problem using Tabulation Approach

## Approach

For **tabulation(down -> top)**, first delcare the same dp array and base case. For base case, when **(ind == 0), T = 0,1,2,...., amount**.

Then, turn the changing variable in the **loop**, i.e., **(1 -> n-1) for ind** and **(0 -> amount) for T**. Then, **copy** the recursion and modify it.

## Code

```c++
    int change(int amount, vector<int>& coins) {
        int n = coins.size();

        vector<vector<int>> dp(n, vector<int>(amount+1, 0));
        for(int i=0;i<=amount; i++) dp[0][i] = (i % coins[0] == 0);

        for(int ind=1; ind<n; ind++){
            for(int j=0; j<=amount; j++){
                int not_take = dp[ind-1][j];
                int take = 0;
                if(coins[ind] <= j) take = dp[ind][j - coins[ind]];
                dp[ind][j] = (not_take + take);
            }
        }
        return dp[n-1][amount];
    }
```

**TC:** O(n\*amount)

**SC:** O(n\*amount)
